
### Pre kitkat way of things
On Android 4.3 and lower, if you want your app to retrieve a file from another app, it must invoke an intent such as ACTION_PICK or ACTION_GET_CONTENT. The user must then select a single app from which to pick a file and the selected app must provide a user interface for the user to browse and pick from the available files
The SAF makes it simple for users to browse and open documents, images, and other files across all of their their preferred document storage providers. A standard, easy-to-use UI lets users browse files and access recents in a consistent way across apps and providers.

### Post-kitkat way of things (i.e using Storage Access framework)

The interaction starts when an application (in this example, a photo app) fires the intent `ACTION_OPEN_DOCUMENT` or `ACTION_CREATE_DOCUMENT`. The intent can include filters to further refine the criteria—for example, "give me all openable files that have the 'image' MIME type."

#### ACTION_GET_CONTENT vs ACTION_OPEN_DOCUMENT

Use `ACTION_GET_CONTENT` if you want your app to simply read/import data. With this approach, the app imports a copy of the data, such as an image file.
Use `ACTION_OPEN_DOCUMENT` if you want your app to have long term, persistent access to documents owned by a document provider. An example would be a photo-editing app that lets users edit images stored in a document provider.

### Processing results

After the user selects a document in the picker, `onActivityResult()` gets called. The `resultData` parameter contains the URI that points to the selected document. Extract the URI using `.getData()` on intent parameter. When you have it, you can use it to retrieve the document the user wants

Central concepts:

### Documents Provider

### Client App

### Picker

