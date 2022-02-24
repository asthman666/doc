Using npm to view node version of the package:    

    npm view prettier engines
    { node: '>=10.13.0' }

    npm view prettier@1.19.1 engines
    { node: '>=4' }

    npm i prettier@1.19.1    

    npx prettier --write .\src\common\apiUtility.js