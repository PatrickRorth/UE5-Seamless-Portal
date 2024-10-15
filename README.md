# UE5-Seamless-Portal (FPS)
Unreal Engine 5 - Seamless Portal / Teleport



![Skrmoptagelse2024-10-15182743-ezgif com-video-to-gif-converter](https://github.com/user-attachments/assets/34d747b4-4ea7-4e63-8f0d-43e868f2ff83)






## Easy Setup
It may seems like there needs to be done a lot, to get this to work, but it only takes like 30sec to do this.

You will even be able to remember what needs to be done, to implement this into another project later on.

## Project settings changes
+ Set these settings as seen below.

![image](https://github.com/user-attachments/assets/08bb65e4-3817-4068-b902-6e6e7f0f02c5)
![image](https://github.com/user-attachments/assets/16be07fe-f389-400d-b8ce-95b7b3cdba61)
![image](https://github.com/user-attachments/assets/56a3f9e4-25ad-4e70-bb58-983453effe62)
![image](https://github.com/user-attachments/assets/146534cb-1479-440a-a964-2af865a126f4)
+ The Anti-Aliasing nees to be either MSAA or FXAA, if not, the portals view will get blurry for some reason. I have not yout found a solution to why this happens.



## Implement into your project
Download the project
Import the **PortalSystem** folder, into your **Content** folder in your UE project
+ You can please the NS_PortalEffect where you want in the Content folder as well



Open your character BP, and create to Variables, of type **Rotator**
+ **InitialWorldRoutation**
+ **InitialControlRoutation**

![image](https://github.com/user-attachments/assets/7b8f1b40-de85-44da-ae60-48ab17026eba)

Copy the blueprint from this link: https://blueprintue.com/blueprint/n9a6e3gc/ and insert it anywhere in the **Event Graph** in your character BP
![image](https://github.com/user-attachments/assets/ae4f39e3-3626-4858-b87d-9fd91019a859)

If you get and error on the Initial xxx Routaiton variables we just created, just drag and drop them, on the notes.

![image](https://github.com/user-attachments/assets/b006558d-6988-43fd-b565-eabf592f8657)

Be sure to drop them on the "background" of the node, and not on the text. **Drop on the green area, and not the red.**
Do this for all the Initial xxx Routation nodes in here. Theres should be 4. The smaller ones, drop on the edge of the node.


The Timeline in the setup you just copyed will fail on the **alpha** node.

+ Alt click the two lines connected to the alpha note, to disconnect them.
+ Double click the Timeline
+ Press the button **+Track** and select **Add Float Track** and name it **alpha**
+ Set the length in top left, to **0.25**
+ Add two new nodes by rightclicking the timeline, and click **Add key to xxx**
+ Select the first one, and set the **Time** and **Value** to **0**
+ Select the second one, and set the **Time** to **0.25** and **Value** to **1**
+ Save and go back to **Event Graph**
+ Your timeline now has a new **alpha** option
+ Connect it to both the **Ease**(Green) node to the right side of the Timeline.

  ![image](https://github.com/user-attachments/assets/be49f506-78f6-46c9-8eb1-185a5d46c02f)

+ Now open the **BP_Portal Blueprint**
+ In the **Functions* list, open **ShouldTeleport?*
+ The **Cast to** will fail, so rightclick and search for the Cast To *BP_FirstPersonCharacter** (Just select what ever your character BP is called)
+ Right click the new node, and select **Convert to pure cast** in the bottom
+ Draw out from the new **Cast To** node, and search for **Get camera view(Camera)** (he camera you are using in your character)
+ Delete the new big node **Get camera new**, but keep the small node with the **Target** and **Camera**
+ Link the **Get Player Character** to the new **Cast to**, and then link the new small node **Camera** to the **Get World Location**
+ Delete the two other notes, that was already linked.

  ![image](https://github.com/user-attachments/assets/c5375743-5b95-442e-8c1c-0843b40428bd)

+ Now open **TeleportCharacter** in the **Functions** list
+ In the top right, of the bluwprint, theres another **Cast to** thats failing, anlong with the **Smooth Oreintation**
+ Do like before, and make a new **Cast to** and convert it to **Pure Cast**
+ Link the **Get Player Character** to the new **Cast to**
+ From the new **Cast to** draw out a line, and search for **Smooth** and select **Smooth Oreintation**
+ Connect the new **Cast to** to the new **Smooth .. Target**
+ Connect the small purple dot into the **New Control Routation** in the **Smooth ..**
+ Just like it was before. When done, delete the old **Cast to** and old **Smooth ..**
+ Compile and save

  ![image](https://github.com/user-attachments/assets/ceaf238b-5c21-43fe-a092-c2497363d8f5)

+ Drag and drop two portals(BP_Portal) into your world.
+ Click Portal 1, and in the **Details** panel under **Linked Portal** select Portal 2
+ Click Portal 2, and in the **Details** panel under **Linked Portal** select Portal 1
+ Thats it.
