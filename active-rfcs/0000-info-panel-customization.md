- Start Date: 2020-05-12
- Reference Issues: N/A
- Implementation PR: N/A

# Summary

Support per project customization of Info Panel.

# Motivation

Raw representation of feature's data may be not always enough. If there is a better way
to represent data, possibility to create a custom project-specific presentation of data
will make application more useful.

# Detailed design

Because web application is built as Vue.js single page application, best integration can
be achieved by using the same tech stack. Vue CLI already out of box supports
[library target build](https://cli.vuejs.org/guide/build-targets.html#library), which allows
to build single or even multiple Vue components as library module. Another useful option
is [css.extract](https://cli.vuejs.org/config/#css-extract) option, which determines whether
CSS styles will be generated in separate file, or included (inlined) in JavaScript code.
This will allow to build custom component(s) (including all dependency libraries)
as single JavaScript file.

With possibility to build custom components, there are basically two options how to use them:

1. Define component for the whole detail content. This option will allow maximal customization,
but may require more coding and reusability may be worse.

2. Define component for single field (attribute). This option can be preffered when default
(generic) view will be suitable for many fields, and only a few fields will require replacement.

But in order to use custom component(s) in the project, it's configuration must be extended
to support this feature, and server will have to provide API to upload and serve JavaScript
files with bundled components. And this depends on building/bundling process. Single component
built as separate JavaScript file is easiest to implement, because you doesn't need to know
module's content. But when you build multiple components into single JavaScript UMD module,
application will need to know mapping of module's properties to Vue components. Analyzing
JavaScript file on server after the upload could be difficult. More likely solution could
be manually written or automatically generated (maybe webpack plugin) metadata file, which
would be also uploaded to the server.

## Project configuration file

## Server API

Gisquick's web apps are built as static pages and served with NGINX. All JS, CSS or image files
are generated with filename hashing feature and with pre-generated compressed versions (gzip).
But because custom components should be attached to particular project, serving them with NGINX
may be not sufficient, especially if access should be restricted by project authentication settings.
Vue CLI also doesn't generates files with hashes for library target build, what would allow
to use max. caching headers for serving. 

#### Upload

**Request**
<table>
  <tbody>
    <tr>
      <td>URL</td>
      <td><code>/api/project/static/{user}/{project}</code></td>
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

#### Serve

**Request**
<table>
  <tbody>
    <tr>
      <td>URL</td>
      <td><code>/api/project/static/{user}/{project}/{file}</code></td>
    </tr>
    <tr>
      <td>Method</td>
      <td><code>GET</code></td>
    </tr>
  </tbody>
</table>

## Map web application
