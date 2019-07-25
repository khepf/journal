The end goal here is relatively straightforward: 
- Take data from an events output, store it in a variable
- create a click event that downloads the data into a txt file

The solution I have so far seems kind of hacky to me. The basic premise here is that we:
- create an invisible a tag
- set element attributes for href and download
- then trigger a click on the a tag
- then delete the a tag.

```
    const element = document.createElement('a');
    if (element.download !== undefined) {
      element.setAttribute(
        'href',
        'data:text/json;charset=utf-8,' +
          encodeURIComponent(JSON.stringify(logDataOrdered))
      );
      element.setAttribute('download', downloadName);
      element.style.visibility = 'hidden';
      document.body.appendChild(element);
      element.click();
      document.body.removeChild(element);
    }
```

Referenced:
https://ourcodeworld.com/articles/read/189/how-to-create-a-file-and-generate-a-download-with-javascript-in-the-browser-without-a-server

https://stackoverflow.com/questions/3665115/how-to-create-a-file-in-memory-for-user-to-download-but-not-through-server

Added support for IE11:

```
// IE10+ : (has Blob, but not a[download] or URL)
if (navigator.msSaveBlob) {
    return navigator.msSaveBlob(blob, fileName);
}
```
https://stackoverflow.com/questions/18394871/download-attribute-on-a-tag-not-working-in-ie




