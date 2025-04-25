# Standalone Company Phone Number Finder

A Python script to find potential contact phone numbers for a company using its name or domain. It utilizes a SearXNG instance for web searching and regular expressions to extract numbers.

## Features

* Finds potential phone numbers associated with a company.
* Accepts company name or company domain/URL as input.
* Uses a SearXNG instance for privacy-respecting web searches.
* Extracts North American-style phone numbers from search result titles and snippets.
* Formats extracted numbers consistently (e.g., `+1-XXX-XXX-XXXX`).
* Handles domain sanitization.
* Removes duplicate numbers.
* Outputs results as a JSON list.
* Standalone script design.
* Configurable logging level.

## Prerequisites

1. **Python:** Python 3.7+ recommended.
2. **Pip:** Python package installer.
3. **SearXNG Instance:** Access to a running SearXNG instance (self-hosted or public). Note its base URL.

## Installation

1. **Clone the repository or download the script:**
2. ```bash
   git clone https://github.com/Aboodseada1/Phone-Finder
   cd https://github.com/Aboodseada1/Phone-Finder
   ```
3. Or simply download the `standalone_phone_finder.py` file.
4. **Install required Python package:**
5. ```bash
   pip install requests
   ```
6. *(Optional but recommended)* Use a Python virtual environment:
7. ```bash
   python -m venv venv
   source venv/bin/activate # On Windows use `venv\Scripts\activate`
   pip install requests
   ```

## Usage

The script is run from the command line:

```bash
python standalone_phone_finder.py <company_input> --searx-url <searx_instance_url> [options]
```

**Arguments:**

* `company_input`: (Required) The company name (e.g., `"Example Corp"`) or domain/URL (e.g., `example.com`). Wrap names with spaces in quotes.
* `--searx-url`: (Required) The base URL of your running SearXNG instance (e.g., `http://127.0.0.1:8080`).
* `--log-level`: (Optional) Set the logging level. Choices: `DEBUG`, `INFO`, `WARNING`, `ERROR`. Default is `INFO`.

## Examples

*(Replace placeholders)*

```bash
# Find phone numbers for a company name
python standalone_phone_finder.py "Google" --searx-url "http://localhost:8080"

# Find phone numbers using a domain
python standalone_phone_finder.py "microsoft.com" --searx-url "https://searx.example.org"

# Run with debug logging
python standalone_phone_finder.py "ACME Corporation" --searx-url "http://127.0.0.1:8080" --log-level DEBUG
```

## Output Format

The script outputs a JSON object containing a list of found phone numbers (or an empty list if none are found) under the `phone_numbers` key. If an error occurs, an `error` key may also be present.

### Example Success Output:

```json
{
  "phone_numbers": [
    "+1-800-555-0100",
    "+1-888-555-0199"
  ]
}
```

### Example No Results Output:

```json
{
  "phone_numbers": []
}
```

## How It Works

1. **Input Processing:** Determines if the input is likely a domain or company name. Sanitizes domains/URLs.
2. **Query Generation:** Creates search queries targeting contact information (e.g., `<company> contact phone number`).
3. **SearXNG Search:** Uses the provided SearXNG instance URL to fetch search results for the queries.
4. **Extraction:** Scans the titles and content snippets from search results using a regular expression designed for common North American phone number formats.
5. **Formatting & Deduplication:** Formats valid numbers into a consistent `+1-XXX-XXX-XXXX` pattern and removes duplicates.
6. **Output:** Returns the unique, formatted phone numbers as a JSON list.

## Limitations

* The phone number extraction regex is primarily focused on **North American (US/Canada)** formats. It may miss or misinterpret international numbers.
* Accuracy depends heavily on the quality and availability of contact information in the SearXNG search results.
* It extracts numbers found directly in search snippets, which might not always be the primary or desired contact number.

## Dependencies

* `requests`

## Contributing

Contributions, especially improvements to the phone number regex for wider international support, are welcome! Please feel free to open an issue or submit a pull request on [GitHub](https://github.com/Aboodseada1?tab=repositories).

## Support Me

If you find this tool useful, consider supporting its development via [PayPal](http://paypal.me/aboodseada1999). Thank you!

## License

This project is licensed under the MIT License.

```
MIT License

Copyright (c) 2025 Abood

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
