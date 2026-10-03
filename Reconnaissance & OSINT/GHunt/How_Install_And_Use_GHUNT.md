# How to Install and Use GHUNT

```text
     .d8888b.  888    888                   888
    d88P  Y88b 888    888                   888
    888    888 888    888                   888
    888        8888888888 888  888 88888b.  888888
    888  88888 888    888 888  888 888 "88b 888
    888    888 888    888 888  888 888  888 888
    Y88b  d88P 888    888 Y88b 888 888  888 Y88b.
     "Y8888P88 888    888  "Y88888 888  888  "Y888 v2
```

## Installation & Setup Steps

1. **Install `pipx`**: Run the command in your terminal:
   ```bash
   pip install --user pipx
   ```
2. **Ensure PATH / Isolate Environment**: Configure `pipx` path:
   ```bash
   python -m pipx ensurepath
   ```
3. **Install GHunt**: Install GHunt via pipx:
   ```bash
   python -m pipx install ghunt
   ```
4. **Log in to GHunt**: Start the login process:
   ```bash
   ghunt login
   ```
5. **Install Companion Extension**: Use Firefox and install the **GHunt Companion** browser extension.
6. **Log in to Google**: Log in to your personal Google account in the browser.
7. **Authenticate**: When the GHunt login prompts you to authenticate, select **option 3** to authenticate.
8. **Synchronize**: Click **Synchronize to GHunt** on the GHunt Companion extension. This will automate the token setup, and GHunt will be ready to use.

---

## Usage Examples

- **Investigate an Email Address**: Get all possible information about a Gmail address:
  ```bash
  ghunt email example@gmail.com
  ```
- **Export Email Results to JSON**: Save the output to a JSON file:
  ```bash
  ghunt email example@gmail.com --json mine.json
  ```
- **Investigate a Google Drive File/Folder**: Query drive ID or file ID:
  ```bash
  ghunt drive drive_id/file_id (e.g., 1sH_rvohihW1_RJi1kR3) --json oladrive.json
  ```
- **Investigate Google Gaia ID**: Use the 21-digit personal ID to reveal Google Maps reviews and related profile data:
  ```bash
  ghunt gaia <personalID>
  ```
  _(Copy the generated profile link to see more details about the target)._

---

## Common Problems & Fixes (When Installing via Python / Pipx)

If you run into errors in the terminal when installing GHunt, here are the troubleshooting steps and fixes applied:

### 1. Update `email.py`

You may need to locate this file on your system (adjusting the path according to your username/Python version):

- **Path Example**:
  `C:\Users\DELL\AppData\Local\Packages\PythonSoftwareFoundation.Python.3.13_qbz5n2kfra8p0\LocalCache\Local\pipx\pipx\venvs\ghunt\Lib\site-packages\ghunt\modules\email.py`
- Scroll to the beginning of the `async def hunt(...)` function block (around lines 20–25).
- Add default fallback values for `photos`, `reviews`, and `stats` right at the start of the function so Python always knows they exist:
  ```python
  photos = []
  reviews = []
  stats = {}
  ```

### 2. Update `people.py`

Locate the parser file on your system:

- **Path Example**:
  `C:\Users\DELL\AppData\Local\Packages\PythonSoftwareFoundation.Python.3.13_qbz5n2kfra8p0\LocalCache\Local\pipx\pipx\venvs\ghunt\Lib\site-packages\ghunt\parsers\people.py`
- Around line 164 of `people.py`, an error can occur if the user does not have a profile/cover photo. Update the container check logic:
  ```python
  container = cover_photo_data.get("metadata", {}).get("container")
  if container:
      self.coverPhotos[container] = person_cover_photo
  ```

With these adjustments, your GHunt installation should run perfectly.
