---
layout: post
title: Downloading Files With Angular 4
tags:
- angular
---

Saving a file with Angular is a bit tedius when we get the file as a blog from an API call. A traditional way of doing is to open the url in a new window. It can work unless there's no authentication required by the API. In my situation though, the API validated authentication.

An easy way to save the file in this case is to use `file-saver` library. It's not an angular variant but works. One aspect to focus on here is to wrap out third party libraries that we might replace in the future.

## File Downloader

Make sure you install `file-saver` first.

```
npm install --save file-saver
```

So, here's my file downloader. It wraps the `file-saver` functionality so that we don't depend on the library in 10 different places. 

*file-download-helper.ts*
```typescript
import { saveAs } from 'file-saver/FileSaver';
import { Response } from '@angular/http';

/**
 * Saves a file by opening file-save-as dialog in the browser
 * using file-save library.
 * @param blobContent file content as a Blob
 * @param fileName name file should be saved as
 */
export const saveFile = (blobContent: Blob, fileName: string) => {
    const blob = new Blob([blobContent], { type: 'application/octet-stream' });
    saveAs(blob, fileName);
};

/**
 * Derives file name from the http response
 * by looking inside content-disposition
 * @param res http Response
 */
export const getFileNameFromResponseContentDisposition = (res: Response) => {
    const contentDisposition = res.headers.get('content-disposition') || '';
    const matches = /filename=([^;]+)/ig.exec(contentDisposition);
    const fileName = (matches[1] || 'untitled').trim();
    return fileName;
};
```

## Using In a Service

Here's an example of the above helper being used in a service.
Notice the service here downloads the file content and then uses our helper to trigger *save as*. My `InterceptorService` is an http intercepter that will attach the **Bearer Token** to the request. Thus the api is able to authenticate the user.

```typescript
import { Injectable } from '@angular/core';
import { RequestOptions, ResponseContentType } from '@angular/http';
import { Observable } from 'rxjs/Observable';
import { InterceptorService } from 'ng2-interceptors';

import { ConfigService } from 'app/common/services/config.service';
import { getFileNameFromResponseContentDisposition, saveFile } from 'app/core/helpers/file-download-helper';

@Injectable()
export class FileService {
    constructor(
        private config: ConfigService,
        private http: InterceptorService,
    ) {}

    downloadFile(propertyId: string, fileId: string) {
        const url = `${this.config.baseUrl}/properties/${propertyId}/files/${fileId}`;
        const options = new RequestOptions({responseType: ResponseContentType.Blob });

        // Process the file downloaded
        this.http.get(url, options).subscribe(res => {
            const fileName = getFileNameFromResponseContentDisposition(res);
            saveFile(res.blob(), fileName);
        });
    }
}
```

Neat! there you go. You could use this Service from a Component just like any other service.