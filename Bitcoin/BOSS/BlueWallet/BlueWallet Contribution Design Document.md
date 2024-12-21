### Project Brief:

Thin Bitcoin Wallet. Built with React Native and Electrum.

### Project Link:

**GitHub** :

https://github.com/BlueWallet/BlueWallet.git

### Issue Breakdown:

**Title:** Edit fingerprint on wallets/details for HD watch-only \#1261

  

**Issue Link**:

https://github.com/BlueWallet/BlueWallet/issues/1261

**Description**

The author of the issue requested that the fingerprint for HD wallets be editable a breakdown of the request can be found below

> [!info] Generate fingerprint for watch only wallet · Issue \#6369 · BlueWallet/BlueWallet  
> Generate fingerprint for watch only wallet  
> [https://github.com/BlueWallet/BlueWallet/issues/6369#issuecomment-2045469187](https://github.com/BlueWallet/BlueWallet/issues/6369#issuecomment-2045469187)  

I have also received approval to work on this issue from the maintainer ==**[Overtorment](https://github.com/Overtorment)**==

### Steps to fix the issue:

- Fork project repo, configure, and run locally following project docs
- Make changes in the file `/BlueWallet/screen/wallets/details.js`, to replace the `BlueText` component with a `TextInput` component to allow users to modify the default value of the auto-generated master fingerprint hex for an imported read-only HD wallet
    
    ```Diff
    - <BlueText>{masterFingerprint ?? <ActivityIndicator />}</BlueText>
    
    + <View style={[styles.input, stylesHook.input]}>
    +  <TextInput
    +    value={masterFingerprint}
    +    numberOfLines={1}
    +    placeholderTextColor="\#81868e"
    +    style={styles.inputText}
    +    editable={!isLoading}
    +    underlineColorAndroid="transparent"
    +    testID="MasterFingerPrintInput"
    +    placeholder={masterFingerprint}
    +   />
    +</View>
    ```
    
- Write some logic to confirm that the new fingerprint hex entered is a valid hex value
- If valid, write a setter method in the `WatchOnlyWallet` class located here `BlueWallet/class/wallets/watch-only-wallet.ts` to update the `masterFingerprint` class variable from its default value of `0` to the wallet owner's new value.
    
    ```TypeScript
    export class WatchOnlyWallet extends LegacyWallet {
      static readonly type = 'watchOnly';
      static readonly typeReadable = 'Watch-only';
      // @ts-ignore: override
      public readonly type = WatchOnlyWallet.type;
      // @ts-ignore: override
      public readonly typeReadable = WatchOnlyWallet.typeReadable;
    
      public _hdWalletInstance?: THDWalletForWatchOnly;
      use_with_hardware_wallet = false;
      
      //Below is the default masterFingerprint value
      masterFingerprint: number = 0;
      
      //....truncated for convenience
      }
    ```
    
- Rebase on master, commit changes, and open a PR

### Conclusion

The scope of these changes for now would be two files and I’d make sure to update this document if that changes.