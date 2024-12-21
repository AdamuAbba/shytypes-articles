### Project Brief:

Sim-ln is a simulation tool that can be used to generate realistic payment activity on any lightning network topology.

### Project Link:

**GitHub** :

https://github.com/bitcoin-dev-project/sim-ln

  

### Issue Breakdown:

**Title:** Error formatting: Go over the displayed errors and make them more user-friendly \#40

  

**Issue Link**:

https://github.com/bitcoin-dev-project/sim-ln/issues/40

  

**Description**

The author of the issue requested that some error messages be reformatted so they are user-friendly as can be seen in his comment here.

> [!info] Error formatting: Go over the displayed errors and make them more user friendly · Issue \#40 · bitcoin-dev-project/sim-ln  
> Just as an example, if a destination node does not support keysend, this is the error we&\#39;ll be getting: Error: Lightning Error: ValidationError(&quot;Destination node does not support keysend 0.  
> [https://github.com/bitcoin-dev-project/sim-ln/issues/40#issue-1855153135](https://github.com/bitcoin-dev-project/sim-ln/issues/40#issue-1855153135)  

I have also received approval to work on this issue from ==[carlaKC](https://github.com/carlaKC)== via her reaction on my comment

### Steps to fix the issue:

- Fork project repo, configure, and run locally following project docs
- The current implementation for error messages in sim-ln returns errors in the format below
    
    `Error: Lightning Error: ValidationError("Destination node does not support keysend 02ab4734430c485b1d15af93ff00060db86f7fe952b04c19afd42709dcd83b1c50")`
    
    So my job would be to refactor this within the scope of the entire app to look something like this which greatly improves the readability of the error messages.
    
    ```Bash
    Error: Lightning Error
    Type: Validation Error
    Caused by: The destination node does not support keysend
    Destination: 02ab4734430c485b1d15af93ff00060db86f7fe952b04c19afd42709dcd83b1c50
    ```
    
- Rebase on master, commit changes, and open a PR

### Conclusion

A potential constraint is that I am new to the Rust programming language so selecting this project and most especially this issue to work on was intentional to help me get some real-world hands-on experience with the language within a controlled scope. If there are any updates I’ll make sure to keep this design document updated.