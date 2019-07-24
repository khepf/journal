Seems kind of hacky to me. The basic premise here is that we:
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



