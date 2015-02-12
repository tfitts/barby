## Changes
This fork adds a :show_code => true option to svg to output the UPC code below the UPC in
the same format you normally see on items at the store.  I also made adjustments to the
borders making the top border smaller and the bottom border bigger make room for the numbers
below the barcode.  Font size scales with :xdim option.  An example UPC is below.

<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" width="107px" height="52px" viewBox="0 0 107 52" version="1.1">
<title>0726528307307</title>
<g id="canvas">
<rect x="0" y="0" width="107px" height="52px" fill="white"></rect>
<g id="barcode" fill="black">
<rect x="6" y="4" width="1px" height="40px"></rect>
<rect x="8" y="4" width="1px" height="40px"></rect>
<rect x="10" y="4" width="3px" height="40px"></rect>
<rect x="14" y="4" width="2px" height="40px"></rect>
<rect x="18" y="4" width="1px" height="40px"></rect>
<rect x="21" y="4" width="2px" height="40px"></rect>
<rect x="24" y="4" width="1px" height="40px"></rect>
<rect x="26" y="4" width="4px" height="40px"></rect>
<rect x="31" y="4" width="2px" height="40px"></rect>
<rect x="36" y="4" width="1px" height="40px"></rect>
<rect x="39" y="4" width="1px" height="40px"></rect>
<rect x="42" y="4" width="2px" height="40px"></rect>
<rect x="45" y="4" width="2px" height="40px"></rect>
<rect x="48" y="4" width="3px" height="40px"></rect>
<rect x="52" y="4" width="1px" height="40px"></rect>
<rect x="54" y="4" width="1px" height="40px"></rect>
<rect x="56" y="4" width="1px" height="40px"></rect>
<rect x="61" y="4" width="1px" height="40px"></rect>
<rect x="63" y="4" width="3px" height="40px"></rect>
<rect x="68" y="4" width="1px" height="40px"></rect>
<rect x="70" y="4" width="1px" height="40px"></rect>
<rect x="74" y="4" width="1px" height="40px"></rect>
<rect x="77" y="4" width="1px" height="40px"></rect>
<rect x="82" y="4" width="1px" height="40px"></rect>
<rect x="84" y="4" width="3px" height="40px"></rect>
<rect x="89" y="4" width="1px" height="40px"></rect>
<rect x="91" y="4" width="1px" height="40px"></rect>
<rect x="95" y="4" width="1px" height="40px"></rect>
<rect x="98" y="4" width="1px" height="40px"></rect>
<rect x="100" y="4" width="1px" height="40px"></rect>

</g><g id="code_box" fill="white">
<rect x="16" y="39" width="35px" height="7px"></rect>
<rect x="56" y="39" width="35px" height="7px"></rect>
</g>
<g id="code_text_checksum" font-family="Verdana" font-size="9">
<text text-anchor="middle" x="3" y="51">0</text>
<text text-anchor="middle" x="104" y="51">7</text>
</g>
<g id="code_text" font-family="Verdana" font-size="10">
<text text-anchor="middle" x="33" y="47">72652</text>
<text text-anchor="middle" x="74" y="47">83073</text>

</g></g>
</svg>

# Barby
Barby is a Ruby library that generates barcodes in a variety of symbologies.

Its functionality is split into _barcode_ and "_outputter_" objects:
  * [`Barby::Barcode` objects] [symbologies] turn data into a binary representation for a given symbology.
  * [`Barby::Outputter`] [outputters] then takes this representation and turns it into images, PDF, etc.

You can easily add a symbology without having to worry about graphical
representation. If it can be represented as the usual 1D or 2D matrix of
lines or squares, outputters will do that for you.

Likewise, you can easily add an outputter for a format that doesn't have one
yet, and it will work with all existing symbologies.

For more information, check out [the Barby wiki] [wiki].

### New require policy

Barcode symbologies are no longer required automatically, so you'll have to
require the ones you need.

If you need EAN-13, `require 'barby/barcode/ean_13'`. Full list of symbologies and filenames below.

## Example

```ruby
require 'barby'
require 'barby/barcode/code_128'
require 'barby/outputter/ascii_outputter'

barcode = Barby::Code128B.new('BARBY')

puts barcode.to_ascii #Implicitly uses the AsciiOutputter

## #    #  #   # ##   # #   ##   ##   # ### #   # ##   ### ## #   ## ### ### ##   ### # ##
## #    #  #   # ##   # #   ##   ##   # ### #   # ##   ### ## #   ## ### ### ##   ### # ##
## #    #  #   # ##   # #   ##   ##   # ### #   # ##   ### ## #   ## ### ### ##   ### # ##
## #    #  #   # ##   # #   ##   ##   # ### #   # ##   ### ## #   ## ### ### ##   ### # ##
## #    #  #   # ##   # #   ##   ##   # ### #   # ##   ### ## #   ## ### ### ##   ### # ##
## #    #  #   # ##   # #   ##   ##   # ### #   # ##   ### ## #   ## ### ### ##   ### # ##
## #    #  #   # ##   # #   ##   ##   # ### #   # ##   ### ## #   ## ### ### ##   ### # ##
## #    #  #   # ##   # #   ##   ##   # ### #   # ##   ### ## #   ## ### ### ##   ### # ##
## #    #  #   # ##   # #   ##   ##   # ### #   # ##   ### ## #   ## ### ### ##   ### # ##
## #    #  #   # ##   # #   ##   ##   # ### #   # ##   ### ## #   ## ### ### ##   ### # ##
          B          A          R          B          Y
```

## Supported symbologies

```ruby
require 'barby/barcode/<filename>'
```

| Name                                | Filename              | Dependencies  |
| ----------------------------------- | --------------------- | ------------- |
| Code 25                             | `code_25`             | ─             |
| ├─ Interleaved                      | `code_25_interleaved` | ─             |
| └─ IATA                             | `code_25_iata`        | ─             |
| Code 39                             | `code_39`             | ─             |
| Code 93                             | `code_93`             | ─             |
| Code 128                            | `code_128`            | ─             |
| └─ GS1 128                          | `gs1_128`             | ─             |
| EAN-13                              | `ean_13`              | ─             |
| ├─ Bookland                         | `bookland`            | ─             |
| └─ UPC-A                            | `ean_13`              | ─             |
| EAN-8                               | `ean_8`               | ─             |
| UPC/EAN supplemental, 2 & 5 digits  | `upc_supplemental`    | ─             |
| QR Code                             | `qr_code`             | `rqrcode`     |
| DataMatrix (Semacode)               | `data_matrix`         | `semacode`    |
| PDF417                              | `pdf_417`             | JRuby         |


## Outputters

```ruby
require 'barby/outputter/<filename>_outputter'
```

| filename    | dependencies  |
| ----------- | ------------- |
| `ascii`     | ─             |
| `cairo`     | cairo         |
| `html`      | ─             |
| `pdfwriter` | ─             |
| `png`       | chunky_png    |
| `prawn`     | prawn         |
| `rmagick`   | RMagick       |
| `svg`       | ─             |

### Formats supported by outputters

* Text (mostly for testing)
* PNG, JPEG, GIF
* PS, EPS
* SVG
* PDF
* HTML

---

For more information, check out [the Barby wiki] [wiki].


  [wiki]: https://github.com/toretore/barby/wiki
  [symbologies]: https://github.com/toretore/barby/wiki/Symbologies
  [outputters]: https://github.com/toretore/barby/wiki/Outputters
