- Start Date: 2020-04-26
- Reference Issues: N/A
- Implementation PR: N/A

# Summary

Allow uploading & serving of media files (images, documents, ...) into the project,
so you can store their links in attributes data of vector layers and view/download
them from web application.

# Motivation

Allow to store images (or other files) directly on Gisquick server along with rest of project's data.
Built-in solution can give us full control and possibility to adjust it for clients needs.

# Detailed description

When user identify features or open attribute table and use Info Panel for displaying
feature's attributes, fields associated with media file type will be displayed as images
or hyperlinks. If layer will be editable and user will enable edit mode, these fields
will allow to upload a new file (or select from already uploaded files).

# Detailed design

There will be fixed-named folder, e.g. *media/* inside project's folder. Web application will be
able to upload files into that folder through http API, and will be able to display file's content
or download it.

## Server API

Server will have following endpoints:

#### Upload

Upload a new project's media file

Requirements:
- respect project size limit
- return link of media file
- check permissions? (use layer's permissions, or new separate configuration per media folder?)
- how to handle filenames?
- support multiple files upload?

**Request**
<table>
  <tbody>
    <tr>
      <td>URL</td>
      <td><code>/api/project/media/{user}/{project}</code></td>
    </tr>
    <tr>
      <td>Method</td>
      <td><code>POST</code></td>
    </tr>
    <tr>
      <td>Content-Type</td>
      <td><code>multipart/form-data</code></td>
    </tr>
  </tbody>
</table>

**Response**
<table>
  <tbody>
    <tr>
      <td>Content-Type</td>
      <td><code>text/plain</code>, or <code>application/json</code>?</td>
    </tr>
  </tbody>
</table>

#### Serve

Get content of project's media file

Requirements:
- Content-Type header by type of the file
- limit access? how?

**Request**
<table>
  <tbody>
    <tr>
      <td>URL</td>
      <td><code>/api/project/media/{user}/{project}/{file}</code></td>
    </tr>
    <tr>
      <td>Method</td>
      <td><code>GET</code></td>
    </tr>
  </tbody>
</table>

#### Delete

Do we need API for deleting files?

### Implementation

Probably best place for implementation of this API is gisquick/settings service.


## Project configuration

### Layer attribute configuration

In addition to current *type* attribute, we will need to extend attribute's configuration.
Something like this:

```javascript
{
  "alias": "Image",
  "name": "image",
  "type": "TEXT(254)",
  "meta": {
    "widget": "ProjectMediaFile",
    "accept": "image/*",
    "prefix": "streets/",
    "multiple": false
  }
}
```
Final format should be ideally designed to be consistent with other features, like
customization of Info Panel.

## Map web application

### Viewing files

Viewing images or providing download links in app is not difficult.
Fields associated with media file type will need to store text links in right format,
e.g. `/media/{user}/{project}/{file}`, and project configuration needs to be
extended with additional info in order to interpret its data values (text data type)
as media file. Then it will be possible to create and use a new component,
which will interpret media file link as **img** or **a** HTML element with URL
pointing to API serve endpoint.

### Editing files

In edit mode, a more complicated special field component for upload must be used
(and implemented).

Uploading of files on save can be implemented with slight change in FeatureEditor component,
by adding support of functions (async or normal) as possible values from field components.
And before using value from field component in update (WFS request), there will be check for
function type, with resolving this function to actual value stored as attribute data (link
of media file returned from API upload request).

While uploading of new files is not so difficult, replacing or deleting of existing files
can be more tricky, and depends on how much of files sharing will be allowed. If there will
be possibility to select existing media file in edit form, then the same file can be referenced
from multiple places (other feature from the same (or different) layer). Also additinal extending
of FeatureEditor would be needed to handle this use cases. 

## Settings web application

Some configuration could be used from QGIS project - Attributes Form, but I expect some Gisquick
specific settings to be still needed. Currently we do not have any attributes configuration page,
so this will be needed to designed and implemented (preferably with other features in mind).

# Drawbacks

N/A

# Alternatives

Rely on external files storage services only.

# Unresolved questions

- Selection from already uploaded files? Will be needed generating of thumbnails for optimal images preview?
- Support multiple files in single field?
- Requirements for deleting/replacing of existing files, which also relates to filenaming strategy
- Requirements for access rules/permissions
