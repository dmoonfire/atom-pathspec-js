atom-pathspec
=============

A utility library for [Atom](https://atom.io/) for resolving relative links into special folders such as the installation directory or the user's home directory. This uses a special "pseudo drive" prefix on the directory to translate into an absolute path.

Prefix         | Location
-------------- | ------------------------------------------------
`application:` | The directory the application is installed into.
`home:`        | The current user's home directory.
`~`            | Same as `home:`.
`config:`      | The configuration folder.
`desktop:`     | The user's desktop.
`documents:`   | The user's documents (My Documents) folder.
`downloads:`   | The user's download folder.
`project:`     | Only used with `getProjectPath()`, gets the project root relative to the given buffer.

The above prefixes are case-insensitive and strip out dashes so `APPDATA:`, `appdata:` and `app-data:` all resolve to the application data directory. This is to make it more tolerant toward non-technical users entering data.

Any leading slashes (`/`) after the colon (or `~`) will be stripped off and the remaining path will be treated as a file relative to that location. For example, on Unix, `home:etc/dictionaries` would resolve to `$HOME/etc/dictionaries`. `home:/etc/dictionaries` and `home://etc/dictionaries` resolve to the same path.

Absolute paths are passed in. If a relative path is given, either by prefixing with a `./` or not having a leading slash or drive, then relatively to the current working drive will be used.

## API

### getPath(spec) => `string`

Returns an absolute path from the given spec.

Param | Type     | Description
----- | -------- | ------------
spec  | `string` | A path specifier which may be an absolute, pseudo-drive, or relative path. |
