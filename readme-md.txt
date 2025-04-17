# Encryption Basics Book

This repository contains a Jupyter Book on encryption basics. The book covers fundamental encryption concepts, historical ciphers, and their applications.

## Book Content

- Introduction to encoding vs. encryption
- Basic encryption algorithms (Caesar, XOR, Vigenère)
- Visual explanations of cryptographic concepts
- Examples and illustrations

## Building the Book

To build the book locally:

1. Clone this repository
2. Install the required packages:
   ```
   pip install -r requirements.txt
   ```
3. Build the book:
   ```
   jupyter-book build .
   ```

The built book will be in the `_build/html/` directory.

## Deploying to GitHub Pages

To deploy the book to GitHub Pages:

1. Build the book as described above
2. Use ghp-import to push the built book to the gh-pages branch:
   ```
   ghp-import -n -p -f _build/html
   ```

Your book will be available at `https://[your-username].github.io/[repository-name]/`

## Contributing

Feel free to contribute by suggesting edits, opening issues, or submitting pull requests.
