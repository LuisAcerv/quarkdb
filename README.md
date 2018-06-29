# Quark DB
Simple JSON db implemented for local storage in electron projects

## Installation

`npm install --save quarkdb`

## Usage

### Instantiation
```javascript
const quarkDb = require('quarkdb');
const db = new quarkDb('/path/to/your/database.json');
```

The prototype of the constructor is `new quarkDb(string, [object])`, and you can supply the optional `options` object by giving it as second parameter:

```
const db = new quarkDb('/path/to/your/database.json', { ... });
```

See the [Options](#options) section for more details.

#### Options

| **Key**     | **Value type** | **Description**                                                | **Default value**                   |
|-------------|----------------|----------------------------------------------------------------|-------------------------------------|
| asyncWrite  | _Boolean_      | Enables the storage to be asynchronously written to disk.      | _**false**_ (synchronous behaviour) |
| syncOnWrite | _Boolean_      | Makes the storage be written to disk after every modification. | _**true**_                          |

### Set a key
`db.set('key', 'value');`

The `key` parameter must be a string, `value` can be whatever kind of object can be stored in JSON format. _`JSON.stringify()` is your friend!_

### Get a key
`db.get('key');`

The `key` parameter must be a string. If the key exhists its value is returned, if it doesn't the function returns `undefined`.

### Check a key
`db.has('key');`

The `key` parameter must be a string. If the key exhists `true` is returned, if it doesn't the function returns `false`.

### Delete a key

`db.delete('key');`

The `key` parameter must be a string. The function returns [as per the _delete_ operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/delete#Return_value) if the key exhists, else it returns `undefined`.

### Sync to disk
`db.sync();`

This function writes the JSON storage object to the file path specified as the parameter of the main constructor. Consult the [Options](#options) section for usage details; on default options there is no need to manually invoke it.

### Access JSON storage
`db.JSON();`

This will return **a copy** of the internal JSON storage object, for you to tinker with and loop over.

### Replace JSON storage
`db.JSON({ data });`

Giving a parameter to the `JSON` function makes the object passed replace the internal one. _Be careful, as there's no way to recover the old object if the changes have already been written to disk._

## Tests

Run `npm test` to start the combined Mocha & Chai testing suite.
