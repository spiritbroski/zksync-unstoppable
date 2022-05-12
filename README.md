# Project name
zksync unstoppable - sending using zksync now become easy because you can just put your unstoppable domain name into the input and you will get the ethereum address easily

# Link to working code in a public repo 
https://github.com/spiritbro1/zksync-unstoppable

# Recorded video demo of the integration (max. 3 mins)
https://user-images.githubusercontent.com/62529025/168067101-7b3bcb03-6ce0-4613-ae48-9ccb828555b1.mp4


# Person of contact in case there are any questions
## Discord ID

spiritbro1#1101

## UnstoppableDomain registered account email address 

3aml5sclu@mozmail.com

# Website demo

https://public-spiritbro.vercel.app/

# How to develop

``` bash
# install dependencies
$ bash cli-dev.sh ci

# Populate .env file as of ropsten-beta connection && serve with hot reload at localhost:3000
$ yarn dev
```

# How to deploy to vercel

There are two folder you need to deploy `public` and `functions`, `public` is for the frontend , `functions` is for communicate with alchemy resolution api this is how you deploy the frontend :

``` bash
# install dependencies
$ bash cli-dev.sh ci

# Populate .env file as of ropsten-beta connection && serve with hot reload at localhost:3000
$ yarn ci:prepare:ropsten-beta

# static version generation
$ yarn ci:build:ropsten-beta
# afterward you'll have prepared distributive in /public folder

$ cd public
$ vercel .
```
And for the `functions` folder you need to first deploy it using this:

```bash
$ cd functions
$ vercel .
```

And in your `functions` vercel project environment variable set `API_KEY` to be your alchemy api key

