# Document Templates Repository

## Summary

The Document Templates repository stores document template definitions for use with the [Document Generator service](https://stash.cdk.com/users/tipperp/repos/document-generator/browse).

## Template Organisation

Document templates and their constituent components are organised according to the hierarchy shown below. Mandatory components are signified with an <span style="color:red">\*</span>.

- **templates** folder
  - **TemplateName** - the template identifier, e.g. `NewVehicleInvoice`
    - A **README.md** file describing the type of document that the template will be used to generate.<span style="color:red">\*</span>
    - JSON schema definition file (`TemplateNameSchema.json`) - defines a JSON schema that can be used to describe and validate the structure of the data object that the EJS template is expecting.
      - **Pro tip:** You can use the [JSONSchema.net](https://jsonschema.net/home) site to generate a JSON schema from a sample JSON document.
    - **\_\_GLOBAL\_\_** folder - the document template in this folder will apply to any enterprise for which no enterprise-specific template has been defined
      - The [Embedded Javascript](https://ejs.co/) (EJS) template file (`TemplateName.ejs`) that will be used to transform the JSON source data into the HTML code that is passed to the Document Generator engine.<span style="color:red">\*</span> 
      - The [CSS Paged Media](https://www.w3.org/TR/css-page-3/) file used by the Document Generator engine to convert the generated HTML code into a PDF document (`TemplateName.css`).
      - Additional resource files, e.g: images files (jpg, img) etc.
    - **EnterpriseId** folder - a version of the document template that applies to a specific enterprise
      - EJS template file (`TemplateName.ejs`)<span style="color:red">\*</span>
      - CSS file (`TemplateName.css`)
      - Additional resource files, e.g: images files (jpg, img) etc.

When a request is sent to the Document Generation service to generate a PDF document from a data object, the template name is specified in the `name` query parameter, and the enterprise is specified in the `enterprise` header parameter. The service will first search for an enterprise-specific template matching the specified template name; if one exists, then it will be used to generate the PDF document, otherwise the template in the \_\_GLOBAL\_\_ folder will be used.
