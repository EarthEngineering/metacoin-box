# MetaCoin EarthBox Example

Originally forked from [truffle-box/metacoin](https://github.com/truffle-box/metacoin-box).

### Install EarthBox

If you don't have Node on your Mac/Linux computer, install it using preferably NVM. On Linux/Mac you can run

```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.1/install.sh | bash
```

after open a new terminal and install the version of Node you prefer, for example the stable v10:

```
nvm install lts/dubnium
```

On Windows, you can install Nvm following the instructions at  
https://github.com/coreybutler/nvm-windows

In any case, when you have Node installed, install EarthBox globally:

```
npm i -g earthbox
```

### Configure Network Information for EarthBox

Network configuration is required by EarthBox.
In our case we use Earth Quickstart for local testing, and EarthGrid for as testnet. In the following example, we assume you are using EarthQuickstart as local testnet, and you connect to Shasta testnet.

```
module.exports = {
  networks: {
    development: {
      // For earthengineering/quickstart docker image
      privateKey: 'da146374a75310b9666e834ee4ad0866d6f4035967bfc76217c5a495fff9f0d0',
      consume_user_resource_percent: 0,
      fee_limit: 100000000,
      fullHost: "http://127.0.0.1:9090",
      network_id: "9090"
    },
    shasta: {
      // Ohio testet
      privateKey: process.env.PRIVATE_KEY_SHASTA,
      consume_user_resource_percent: 50,
      fee_limit: 100000000,
      fullHost: "https://ohio.earth.engineering",
      network_id: "2"
    }
  }
}
```

In order to run the dApp you don't have to change anything in the `earthbox.js` file.

### Use your own private network

`earthbox migrate` by default will use the `development` network that is set to use Earth Quickstart. In order to test the smart contracts and deploy them you must install Earth Quickstart.

1. [Install Docker](https://docs.docker.com/install/).

2. Run Earth Quickstart:

```
docker run -it --rm -p 9090:9090 --name earth earthengineering/quickstart
```

### EarthBox commands

```
earthbox compile
earthbox migrate --reset
earthbox test
```

### Run the example dApp on Shasta

1. You need an account with some Ohio EARTH .

2. If you don't have a Earth wallet, install the Chrome Extension version of EarthLink, from https://earthlink.earth.engineering and create an account.

3. Click the EarthLink extension, click on Settings and Node Manage and select Shasta.

4. If you don't have any Ohio EARTH, open https://faucet.earth.engineering and require some Ohio EARTH at the bottom of the page.

5. Add a file called `.env` in the root of this repo and edit it, adding a line with your Private Key, somethink like:

```
export PRIVATE_KEY_SHASTA=0122194812081292938435739857438538457349573485358345345934583554
```

and save it. You can find an example in `sample-env`.

6. Set the dApp. The dApp needs to know the address where the MetaCoin contract has been deployed. We have put in the box a special script:

```
npm run setup-dapp
```

It will execute the migration, retrieve the contract address and save it in the file `src/js/metacoin-config.js`. This won't work if does not find the `.env` file.

7. Run the dApp:

```
npm run dev
```

It automatically will open the dApp in the default browser.

8. Enjoy your working Earth dApp!

### What else?

If you have questions, drop me a line on twitter at [@cgcardona](https://www.twitter.com/cgcardona)
