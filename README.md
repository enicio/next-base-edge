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