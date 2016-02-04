# express-typescript-sample
Express を TypeScript で書きたい！

### NodeJS をインストール
https://nodejs.org/
```sh
brew update
brew install nodejs
node -v # v5.5.0
npm -v # 3.5.3
```

準備オッケー :ok_woman:

### Express を動かす
http://expressjs.com/

```sh
npm install express-generator -g
express --version # 4.13.1
express myapp
cd myapp
npm install
DEBUG=myapp:* npm start
```

http://localhost:3000/ みえた :ok_woman:

### TypeScript にしていく
さっきのプロジェクトを TypeScript 仕様にしていく。
このへん参考に（特に後者）

- TypeScriptでNode.jsのexpressを使ってHello worldしてみる - oinume journal
http://oinume.hatenablog.com/entry/using-express-with-typescript
- czechboy0/Express-4x-Typescript-Sample: Starter-Kit Node.js Express 4.x app written in TypeScript
https://github.com/czechboy0/Express-4x-Typescript-Sample

とりあえず素の express をコミット
```sh
git init
gibo node >> .gitignore
git add .
git commit -m 'initial commit'
```
tsd install は package.json を見ながら指定する
```sh
npm install typescript tsd --save
./node_modules/.bin/tsd install body-parser cookie-parser debug express jade morgan serve-favicon --save
```
ソースをいろいろいじって…
コンパイルして同じように起動してみる
```sh
./node_modules/.bin/tsc --sourcemap --module commonjs ./bin/www.ts
DEBUG=myapp:* npm start
```
http://localhost:3000/ ｷﾀ━━(ﾟ∀ﾟ)━━!!
gitignore を整えてコミット
```sh
cat << FOO >> .gitignore
typings
**/*.js
**/*.js.map
FOO
git add .
git commit -m 'typescriptized'
```
ちなみにこれでも起動した
```sh
DEBUG=myapp:* node ./bin/www.js
```

### より便利にしたい
tsconfig.json ってやつを作っておくと、コンパイルコマンドが簡潔になってよさそう

- TypeScriptSamples/tsconfig.json at master · Microsoft/TypeScriptSamples
https://github.com/Microsoft/TypeScriptSamples/blob/master/imageboard/tsconfig.json

```sh
./node_modules/.bin/tsc --init --sourcemap --module commonjs ./bin/www.ts
```
こうしておくと、このプロジェクトをコンパイルしたい人は、オプションなしの `tsc` を発動するだけでよくなる（んだと思う）
