<div style="display: flex; align-items: center; justify-content: space-between;">
  <h1>Note on null fields and placeholder values
</h1>
  <img src="rhs-logo_4x4.jpeg" alt="Rec Hockey League Logo" style="width: 100px; height: 100px; margin-left: 20px;">
</div>

When setting up your database, you may not have data for all the fields.
You can handle this in a number of different ways depending on your personal
preferences and the field data type.

You can use the following values as placeholders for data you plan to update later:

**For Strings:** `null`, `""` (empty string), and `"TBD"` are all acceptable placeholders; but an empty field will not be accepted.

**For Integers:** `null`, `""` (empty string), and `"TBD"` are all acceptable placeholders; but an empty field will not be accepted.

**For Boolean:** `null`, `""` (empty string), and `"TBD"` are all acceptable placeholders; but an empty field will not be accepted.

**For Arrays:** `null`, `""` (empty string), and `"TBD"` are all acceptable placeholders; but an empty field will not be accepted.

**NOTE** If you pass a team `id` as `null`, `json-server` will automatically generate the id for you

### [Back to Main Menu](nav.md)