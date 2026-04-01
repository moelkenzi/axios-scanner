# Axios Suspicious Version Scanner

This is a simple, fast, and effective Rust-based tool to scan your system for potentially suspicious versions of the `axios` NPM package.

## Why?

Certain versions of `axios` have been flagged as suspicious. This tool helps you quickly identify if any of your projects are using these versions. The versions currently flagged as suspicious are:

- `1.14.1`
- `0.30.4`

## How it Works

The scanner performs two main checks:

1.  **Direct `axios` Package Scan:** It looks for `axios` installations within `node_modules` directories and checks the `version` specified in their `package.json` file.

2.  **Lockfile Scan:** It scans `package-lock.json` files to see if they contain references to the suspicious `axios` versions.

To improve performance, the scanner is multi-threaded and skips common large or irrelevant directories such as:

- `.git`
- `node_modules/.cache`
- `target` (for Rust projects)
- `Library` (on macOS)

## Scanning Locations

The tool scans the following common development directories:

- `/Users` (on macOS)
- `/home` (on Linux)
- `/root`
- `/var/www`
- `/opt`

## How to Use

1.  **Build the project:**

    ```bash
    cargo build --release
    ```

2.  **Run the scanner:**
    ```bash
    ./target/release/axios_scanner_2
    ```

## Interpreting the Output

- If suspicious versions are found, the tool will print a `⚠️ FOUND` message with the path to the file.
- If no suspicious versions are found, it will print a `✅ No suspicious axios versions found.` message.

If a suspicious version is detected, the tool will provide recommendations on how to resolve the issue.

## Disclaimer

This tool is provided as-is. Always perform your own due diligence and audit your dependencies.
