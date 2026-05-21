# nuclei-project

Custom [Nuclei](https://github.com/projectdiscovery/nuclei) templates for technology detection and security reconnaissance.

## Templates

### `claude-code-wordpress-detect.yaml`
Detects WordPress installations by fingerprinting `/wp-content/` and `/wp-includes/` paths in the response body. Also extracts the WordPress version from the `<meta name="generator">` tag when present.

### `claude-code-robots-sensitive.yaml`
Fetches `/robots.txt` and flags any `Disallow`/`Allow` entries that point to sensitive paths such as admin panels, backup directories, config files, API endpoints, and version control folders. Extracts and displays the matched paths in the output.

### `apache-hertzbeat-scriptcommand-rce.yaml`
Detects authenticated remote code execution in Apache HertzBeat 1.8.0 via the `scriptCommand` parameter. Authenticates with default credentials (`admin:hertzbeat`), overwrites the `linux_script` monitoring template to inject an OOB payload, then triggers execution by creating a monitor instance. Detection is confirmed via interactsh DNS/HTTP callback. Severity: critical. Reference: [EDB-52563](https://www.exploit-db.com/exploits/52563).

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
