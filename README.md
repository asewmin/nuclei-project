# nuclei-project

Custom [Nuclei](https://github.com/projectdiscovery/nuclei) templates for technology detection and security reconnaissance.

## Templates

### `claude-code-wordpress-detect.yaml`
Detects WordPress installations by fingerprinting `/wp-content/` and `/wp-includes/` paths in the response body. Also extracts the WordPress version from the `<meta name="generator">` tag when present.

### `claude-code-robots-sensitive.yaml`
Fetches `/robots.txt` and flags any `Disallow`/`Allow` entries that point to sensitive paths such as admin panels, backup directories, config files, API endpoints, and version control folders. Extracts and displays the matched paths in the output.

## Usage

Run a single template against a target:
```bash
nuclei -u https://target.com -t claude-code-wordpress-detect.yaml -nc
nuclei -u https://target.com -t claude-code-robots-sensitive.yaml -nc
```

Run all templates in this repo against a target:
```bash
nuclei -u https://target.com -t . -nc
```

## Requirements
- [Nuclei](https://github.com/projectdiscovery/nuclei) v3.0+
