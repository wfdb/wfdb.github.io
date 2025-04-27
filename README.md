# WFDB Website

This repository contains the source code for the official Waveform Database (WFDB) project website, built using [Jekyll](https://jekyllrb.com/) and the [Just the Docs](https://just-the-docs.github.io/just-the-docs/) theme. The site serves as a central resource for the WFDB community, providing:

- A specification for the WFDB format.
- An overview of WFDB software implementations.

The website is hosted at [https://wfdb.io](https://wfdb.io).

## About WFDB

The Waveform Database (WFDB) is a set of open file format standards for physiological waveform and annotation data. Originally developed by George B. Moody in 1989 at the Harvard-MIT Division of Health Sciences and Technology, WFDB has become a widely adopted standard in the field of biomedical signal processing.

WFDB files typically consist of:

- **Header files** (`.hea`): Contain metadata about the recording.
- **Signal files** (`.dat`): Store the waveform data.
- **Annotation files** (`.atr`, `.ann`, etc.): Contain annotations such as beat labels or event markers.

For more details, refer to the [WFDB Format Specification](https://wfdb.io/spec/).

## Repository Structure

- `_config.yml`: Jekyll site configuration.
- `Gemfile`: Ruby gem dependencies.
- `index.md`: Homepage content.
- `spec/`: Contains pages related to the WFDB format specification.
- `software/`: Contains pages describing WFDB software implementations.
- `working-group.md`: Information about the WFDB Working Group.

## Installation

To build and serve the website locally, follow these steps:

1. **Install Ruby and Bundler**

   Ensure you have Ruby installed. Then, install Bundler:

   ```bash
   gem install bundler
   ```

2. **Clone the Repository**

   ```bash
   git clone https://github.com/wfdb/wfdb.github.io.git
   cd wfdb.github.io
   ```

3. **Install Dependencies**

   ```bash
   bundle install
   ```

4. **Serve the Site Locally**

   ```bash
   bundle exec jekyll serve
   ```

   The site will be available at `http://127.0.0.1:4000/`.

## Contributing

Contributions are welcome! If you'd like to contribute to the WFDB website, please fork the repository, make your changes, and submit a pull request. For major changes, please open an issue first to discuss what you'd like to change.

## License

This project is licensed under the [MIT License](LICENSE).
