# Pre-compiled binaries of PDFium

[![Build](https://github.com/ezeep/pdfium-binaries/actions/workflows/build.yml/badge.svg?branch=master)](https://github.com/ezeep/pdfium-binaries/actions/workflows/build.yml)
[![Total downloads](https://img.shields.io/github/downloads/bblanchon/pdfium-binaries/total)](https://github.com/ezeep/pdfium-binaries/releases/)
[![Latest release](https://img.shields.io/github/v/release/bblanchon/pdfium-binaries?display_name=release&include_prereleases)](https://github.com/ezeep/pdfium-binaries/releases/latest/)

This project hosts pre-compiled binaries of the [PDFium library](https://pdfium.googlesource.com/pdfium/), an open-source library for PDF manipulation and rendering.

Builds are triggered manually, if needed

**Disclaimer**: This project isn't affiliated with Google or Foxit.

## Download

Here are the download links for latest release:

<table>
  <tr>
    <th>OS</th>
    <th>CPU</th>
    <th>PDFium</th>
  </tr>

  <tr>
    <td rowspan="3">Windows</td>
    <td>x64</td>
    <td><a href="https://github.com/ezeep/pdfium-binaries/releases/latest/download/pdfium-win-x64.tgz">pdfium-win-x64.tgz</a></td>
  </tr>
</table>

See the [Releases page](https://github.com/ezeep/pdfium-binaries/releases) to download older versions of PDFium.

## Documentation

### PDFium API documentation

Please find the [documentation of the PDFium API on developers.foxit.com](https://developers.foxit.com/resources/pdf-sdk/c_api_reference_pdfium/index.html).

### How to use PDFium in a CMake project

1. Unzip the dpwnloaded package in a folder (e.g., `C:\Libraries\pdfium`)
2. Set the environment variable `PDFium_DIR` to this folder (eg `C:\Libraries\pdfium`)
3. In your `CMakeLists.txt`, add

        find_package(PDFium)

4. Then link your executable with PDFium:

        target_link_libraries(my_exe pdfium)

5. On Windows, make sure that `pdfium.dll` can be found by your executable (copy it on the same folder, or put in on the `PATH`).

### How to use JavaScript V8 enabled binaries

If you are using the V8-enabled binaries, additional initialization is required.
In your code, before using PDFium you have to call `FPDF_InitEmbeddedLibraries()`
from the additional header `fpdf_libs.h`, which is only available in V8 enabled
binaries.

The archive will contain a `res` folder which you have to distribute with your
application. On macOS, you should include this in your application bundle for other
platforms place it where your application binary will find it.

See the following example for usage:

```c++
#include "fpdf_libs.h"

...

// Determine the path to files in the res folder from the archive
const char* resPath = "<path to the res folder>";

// Initialize V8 and other embedded libraries
FPDF_InitEmbeddedLibraries(resPath);

// Make use of PDFium
FPDF_InitLibrary();
FPDF_DestroyLibrary();
```

## Related projects

The following project use (or recommend using) our PDFium builds:

* [dart_pdf](https://github.com/DavBfr/dart_pdf), PDF creation module for dart/flutter
* [Flutter native_pdf_renderer](https://github.com/rbcprolabs/packages.flutter/tree/master/packages/native_pdf_renderer), Flutter Plugin to render PDF pages as images
* [PDFium RS](https://github.com/asafigan/pdfium_rs), a Rust wrapper around PDFium
* [PDFiumCore](https://github.com/Dtronix/PDFiumCore), .NET Standard P/Invoke bindings for PDFium
* [PyPDFium2](https://github.com/pypdfium2-team/pypdfium2), Python bindings to PDFium
* [wxPDFView](https://github.com/TcT2k/wxPDFView), wxWidgets components to display PDF content

*Did we miss a project? Please open a PR!*  