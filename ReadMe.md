
# PDF Invoice Template

### ORIGINAL MADE BY Edisonneza on Github.

[Edisonneza GitHub Profile](https://github.com/edisonneza)   
[Original Project Repo](https://github.com/edisonneza/jspdf-invoice-template/blob/main/README.md?plain=1)  
[Youtube Tutorial](https://www.youtube.com/watch?v=GbZa9s9Siss) <i>(5 min)</i>  



## Original ReadMe Content:
To fix Angular v13 and some NodeJs issues, I've separated into two different npm packages, as below:

[For web browsers](https://www.npmjs.com/package/jspdf-invoice-template):    <i>npm i jspdf-invoice-template</i>

[For NodeJs](https://www.npmjs.com/package/jspdf-invoice-template-nodejs):    <i>npm i jspdf-invoice-template-nodejs</i>


PDF template created to generate invoices based on props object. Using `jsPDF` library. ( `jsPDF` is exported also, so it can be used without importing jsPDF separately. )

All this code works by using an object as parameter for the function. <br/>
From <i><b>v1.3.1</b></i> all properties are optional and you can add them as empty string or just remove them from the prop object, if you want to display nothing. Also it can be used in different languages because all labels (and all text) can be set in the props object.

<h4><b><i>Feel free for any suggestion or improvements.</i></b></h4>

## [Demo site](https://edisonneza.github.io/jspdf-invoice-template) | [Demo images](#demo-images) | [jsPDF Documentation](http://raw.githack.com/MrRio/jsPDF/master/docs/) | [Npm](https://www.npmjs.com/package/jspdf-invoice-template) | [Npm NodeJs](https://www.npmjs.com/package/jspdf-invoice-template-nodejs) 
<br/>

# Install and usage
<details open>
<summary>How to install or load in my project?</summary>
This small "library" can be imported in any project via `npm` or in browser via CDN by using `jsPDFInvoiceTemplate` variable. 

Get it from NPM:

```sh
npm i jspdf-invoice-template
```
Or for NodeJs:
```sh
npm i jspdf-invoice-template-nodejs
```

Alternatively, load latest version from a CDN:<br/>
<i>(Recommended to use a static version (not @latest) to prevent failure when updates are made)</i>
```html
<script src="https://unpkg.com/jspdf-invoice-template@1.4.0/dist/index.js"></script>
```
</details>
<hr/>

<details>
<summary>How to use it?</summary>

## Usage

You're ready to start creating your invoice PDF document: 

```javascript
//by importing 
import jsPDFInvoiceTemplate from "jspdf-invoice-template";

//or directly in browser
jsPDFInvoiceTemplate.default( propsObject );


//you can either import the `OutputType` const or `jsPDF` class if you want to create another PDF from scratch (without using the template) 
import jsPDFInvoiceTemplate, { OutputType, jsPDF } from "jspdf-invoice-template";

//or directly in browser
const outputTypes = jsPDFInvoiceTemplate.OutputType;
const jsPDF = jsPDFInvoiceTemplate.jsPDF();

jsPDFInvoiceTemplate.default( propsObject );
```
</details>
<hr/>

<details>
<summary>What about Parameters Object?</summary>

## Parameters object

Just edit the props object and call the function, nothing more... 😊

```javascript
const pdfObject = jsPDFInvoiceTemplate(props); //returns number of pages created

//or in browser
var pdfObject = jsPDFInvoiceTemplate.default(props); //returns number of pages created

var props = {
    outputType: OutputType.Save,
    onJsPDFDocCreation?: (jsPDFDoc: jsPDF) => void, //Allows for additional configuration prior to writing among others, adds support for different languages and symbols
    returnJsPDFDocObject: true,
    fileName: "Invoice 2021",
    orientationLandscape: false,
    compress: true,
    logo: {
        src: "https://raw.githubusercontent.com/edisonneza/jspdf-invoice-template/demo/images/logo.png",
        type: 'PNG', //optional, when src= data:uri (nodejs case)
        width: 53.33, //aspect ratio = width/height
        height: 26.66,
        margin: {
            top: 0, //negative or positive num, from the current position
            left: 0 //negative or positive num, from the current position
        }
    },
    stamp: {
        inAllPages: true, //by default = false, just in the last page
        src: "https://raw.githubusercontent.com/edisonneza/jspdf-invoice-template/demo/images/qr_code.jpg",
        type: 'JPG', //optional, when src= data:uri (nodejs case)
        width: 20, //aspect ratio = width/height
        height: 20,
        margin: {
            top: 0, //negative or positive num, from the current position
            left: 0 //negative or positive num, from the current position
        }
    },
    business: {
        name: "Business Name",
        address: "Albania, Tirane ish-Dogana, Durres 2001",
        phone: "(+355) 069 11 11 111",
        email: "email@example.com",
        email_1: "info@example.al",
        website: "www.example.al",
    },
    contact: {
        label: "Invoice issued for:",
        name: "Client Name",
        address: "Albania, Tirane, Astir",
        phone: "(+355) 069 22 22 222",
        email: "client@website.al",
        otherInfo: "www.website.al",
    },
    invoice: {
        label: "Invoice #: ",
        num: 19,
        invDate: "Payment Date: 01/01/2021 18:12",
        invGenDate: "Invoice Date: 02/02/2021 10:17",
        headerBorder: false,
        tableBodyBorder: false,
        header: [
          {
            title: "#", 
            style: { 
              width: 10 
            } 
          }, 
          { 
            title: "Title",
            style: {
              width: 30
            } 
          }, 
          { 
            title: "Description",
            style: {
              width: 80
            } 
          }, 
          { title: "Price"},
          { title: "Quantity"},
          { title: "Unit"},
          { title: "Total"}
        ],
        table: Array.from(Array(10), (item, index)=>([
            index + 1,
            "There are many variations ",
            "Lorem Ipsum is simply dummy text dummy text ",
            200.5,
            4.5,
            "m2",
            400.5
        ])),
        additionalRows: [{
            col1: 'Total:',
            col2: '145,250.50',
            col3: 'ALL',
            style: {
                fontSize: 14 //optional, default 12
            }
        },
        {
            col1: 'VAT:',
            col2: '20',
            col3: '%',
            style: {
                fontSize: 10 //optional, default 12
            }
        },
        {
            col1: 'SubTotal:',
            col2: '116,199.90',
            col3: 'ALL',
            style: {
                fontSize: 10 //optional, default 12
            }
        }],
        invDescLabel: "Invoice Note",
        invDesc: "There are many variations of passages of Lorem Ipsum available, but the majority have suffered alteration in some form, by injected humour, or randomised words which don't look even slightly believable. If you are going to use a passage of Lorem Ipsum, you need to be sure there isn't anything embarrassing hidden in the middle of text. All the Lorem Ipsum generators on the Internet tend to repeat predefined chunks as necessary.",
    },
    footer: {
        text: "The invoice is created on a computer and is valid without the signature and stamp.",
    },
    pageEnable: true,
    pageLabel: "Page ",
};
```
</details>
<hr/>

<details>
<summary>What will be returned?</summary>
The return object depends on parameters object. See the code below:

```typescript
{
    pagesNumber: number, // (always) - number of pages
    jsPDFDocObject: jsPDF, // if (returnJsPDFDocObject: true) - the doc already created. You can use it to add new content, new  pages.
    blob: Blob, // if (outputType: 'blob') - returns the created pdf file as a Blob object. So you can upload and save it to your server. (Idea from a comment on Twitter)
    dataUriString: string, // if (outputType: 'datauristring')
    arrayBuffer: ArrayBuffer // if (outputType: 'arraybuffer')
}

//store it to a variable and use it wherever you want
var pdfCreated = jsPDFInvoiceTemplate.default({ ...parameters });
var blob = pdfCreated.blob;
//...
var pagesNum = pdfCreated.pagesNumber;
var pdfObject = pdfCreated.jsPDFDocObject;
```
</details>
<hr/>

<details>
<summary>How to use the returned jsPDFDocObject?</summary>

```typescript
//example: create a PDF using the template
var pdfCreated = jsPDFInvoiceTemplate.default({ ...parameters });

//add new page or new content -> see jsPDF documentation
pdfCreated.jsPDFDocObject.addPage();
pdfCreated.jsPDFDocObject.text("Test text", 10, 50);
//...

pdfCreated.jsPDFDocObject.save(); //or .output('<outputTypeHere>');
```
</details>

<hr/>

<details>

<summary>What about fonts and special characters?</summary>
You can use the `onJsPDFDocCreation` property arrow function to hook into configuring the jsPDF functionality as soon as it's initialized.


Allowing the support of multiple languages and currencies for your invoice as outlined in [jsPDF documentation](https://rawgit.com/MrRio/jsPDF/master/docs/):
> Use of Unicode Characters / UTF-8:
The 14 standard fonts in PDF are limited to the ASCII-codepage. If you want to use UTF-8 you have to integrate a custom font, which provides the needed glyphs. 

<b>Example Usage:</b>

```typescript
jsPDFInvoiceTemplate({
  //https://github.com/edisonneza/jspdf-invoice-template/issues/20#issuecomment-1859975854
  onJsPDFDocCreation: (doc: jsPDF) => {
      //var font = "...";
      doc.addFileToVFS('LiberationSans-Regular-normal.ttf', font);
      doc.addFont('LiberationSans-Regular-normal.ttf', 'LiberationSans-Regular', 'normal');
      doc.setFont('LiberationSans-Regular');
      
  },
});
```
</details>

<summary>--- Changelog ---</summary>

<details open>
<summary>v.1.4.4</summary>

  * Added Support for modifying fonts by adding direct access to the jsPDF Document Object, this allows the support for additional fonts as well as changing the font for additional languages.
    - In the event additional functionality is required for certain operation it can be injected as a wrapper function for the underlying jsPDF functionality without needed to modify the base source files.
</details>
<details>
<summary>v.1.4.3</summary>

  * Dynamic rows at the end of the table (total, vat, subtotal etc)
  * Added stamp image at the left bottom of the page (image as a qr code)
</details>

<details>
<summary>v.1.4.2</summary>

  * Separated Nodejs and Web based, into two packages
  * Fixed Image and Blob type (for Nodejs)
</details>

<details>
<summary>v.1.4.0</summary>

  * Added compress option
  * Added custom column style (width) - (FYI: Width-> portrait: 210; landscape: 297)
</details>

<details>
<summary>v.1.3.2</summary>

  * Fixed package entry point
</details>
<details>
<summary>v.1.3.1</summary>

  * Added feature to add or remove columns 
  * Dynamic height in all columns
</details>

<details>
<summary>v.1.2.0</summary>

  * Added returnJsPDFDocObject prop
  * Added support for returning different outputs based on output type prop
  * All parameter object properties are now OPTIONAL
  * Return jspdf doc object, so now can be added new content or edited the pdf file and output it in all types that jsPDF library supports. 
</details>

</details>
<hr/>

# Demo images
![portrait version](https://raw.githubusercontent.com/edisonneza/jspdf-invoice-template/demo/images/portrait_mode.PNG)

Landscape:

![portrait version](https://raw.githubusercontent.com/edisonneza/jspdf-invoice-template/demo/images/landscape_mode.PNG)


## 👋


### Development - Generate types
```
npx -p typescript tsc src/index.js --declaration --allowJs --emitDeclarationOnly --outDir dist/src/

npx -p typescript tsc src/index.js --declaration --allowJs --emitDeclarationOnly 
```

Copyright
(c) 2022 Edison Neza, https://github.com/edisonneza/jspdf-invoice-template

Permission to use, copy, modify, and/or distribute this software for any purpose with or without fee is hereby granted, provided that the above copyright notice and this permission notice appear in all copies.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE
LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION
OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION
WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.