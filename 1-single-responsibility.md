# Single Responsibility

> A class should have one, and only one, reason to change.

> A class should have **a single responsibility**.

## When to extract
- *Does* **this class** *need to know how* **this** *works?* If the answer is no, extract it.
- Extract methods that may be called somewhere else. If you're trying to call a controller, you're doing something wrong.

## Good practices
- Persistence, presentation and validation of data should be extracted to their own class.
- You should rely on interfaces to create contracts that concrete classes should satisfy. These classes will then be injected in a constructor or directly in a method.