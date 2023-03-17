# Cloudflare Pages Test
This project aims to test cloudflare nextjs build in azion.

## Prerequisites
* Azion Cells
* Node >= 16
* Docker
* aws cli

## Installing
In root dir, run:
```
npm install
```

## Building to Azion Cells
In root dir, run: 
```
mkdir .vercel
echo '{"projectId":"_","orgId":"_","settings":{}}' > .vercel/project.json
npx --yes vercel@28.16.11 build --prod
```

Then, start the localstack container and upload builded static files to S3:
```
docker run --rm -it -d -p 4566:4566 -p 4510-4559:4510-4559 localstack/localstack

aws s3api create-bucket --bucket storage-bucket --endpoint=http://0.0.0.0:4566
aws s3api list-buckets --query "Buckets[].Name" --endpoint=http://0.0.0.0:4566

aws s3 sync .vercel/output/static s3://storage-bucket/0001a/MY_NEW_VERSION/ --endpoint=http://0.0.0.0:4566
aws s3api list-objects --bucket storage-bucket --query 'Contents[].{Key: Key, Size: Size}' --endpoint=http://0.0.0.0:4566
```

Files are now available in http://0.0.0.0:4566/cells/.

Finally, run the build script:
```
cd custom-builder
npm install
node index.js
```
After that, you can copy the generated file to cells:
```
cp ./out/worker.js PATH_TO_CELLS/js/worker.js
```

cells last commit reference: d50c1724fab55ef86a18044dd8645609779564e5

Now you can run cells in localhost and access the home page.

Access http://localhost:1666/ with header "X-Azion-Run-Function: worker.js" to check the results.
Use a browser extension to add the header if you want to test in a browser.

To setup and run cells in localhost check this [link](https://github.com/aziontech/cells).