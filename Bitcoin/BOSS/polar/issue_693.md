# Design Document: Polar (Feature Request: Minimize to system tray issue No \#693)

***Maintainer approval:** [https://github.com/jamaljsr/polar/issues/693\#issuecomment-1974811001](https://github.com/jamaljsr/polar/issues/693#issuecomment-1974811001)*

## **Issue Description:**

The issue reporter expressed a desire for the Polar app to have the capability to minimize to the system tray. he often finds himself not actively using its functions but still wants the network running in the background so his application can utilize it when needed. By having the option to minimize to the system tray, he could keep the app running while reducing clutter on their desktop and optimizing his workflow.  
issue(URL): [https://github.com/jamaljsr/polar/issues/693\#issue-1636479315](https://github.com/jamaljsr/polar/issues/693#issue-1636479315)

## **Proposed Solution:**

Using the Electron package to implement a feature that hides, shows, and quits the window of the running instance of the Polar application via its system tray context menu on a user's machine. Below is a sample code snippet of the proposed solution

```typescript
const tray \= **new** Tray(icon);

 var contextMenu \= Menu.buildFromTemplate(\[  
   {  
     label: "Minimize to tray",  
     click: function () {  
       *mainWindow*.hide();  
     },  
   },  
   {  
     label: "Maximize window",  
     click: function () {  
       *mainWindow*.show();  
     },  
   },  
   {  
     label: "Quit Polar",  
     click: function () {  
       *mainWindow*.destroy();  
       app.quit();  
     },  
   },  
 \]);

 tray.setToolTip("Some text here.....");  
 tray.setContextMenu(contextMenu);  
};

```
**The proposed solution above will affect the scope of two files at most if the logic is separated into a different file. However, if the logic remains within the same file, it will only affect one file. All changes would also be contained in a single PR**

##  **Technologies/Frameworks:**

The link below shows a list of all the technologies [https://github.com/jamaljsr/polar\#tech-stack](https://github.com/jamaljsr/polar#tech-stack)

### **Testing Plan:**

* Manual testing on Ubuntu (Host), macOS (Host), and Windows (VM)

## **Timeline:**

* Research, Implementation, and opening of PR: Three days or less

## **Core Dependency:**

* **Electron**: since it is a UI-specific feature, my primary focus would be on utilizing the electron package and its modules to handle the application window state

## **Acceptance Criteria:**

* The user should be able to minimize the polar app from the app's system tray context menu.  
* The user should be able to maximize the polar app from the app’s system tray context menu.  
* As a matter of convenience, the user should be able to quit the app from the context menu as well (optional requirement)

## **Conclusion:**

I have been approved by the project maintainer to handle the issue and will begin work immediately. Since this is my first time using Electron, I'm very excited to delve into it and add it to my toolkit as a JavaScript developer

