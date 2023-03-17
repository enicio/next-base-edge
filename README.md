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
To setup and run cells in localhost check this [link](https://github.com/aziontech/cells).