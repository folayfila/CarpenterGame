![Description](Media/CarpenterGame_Showcase.gif)
# CarpenterGame (CA)
The project is a multiplayer game prototype, where players receive orders to create objects of certain type and color; players must then create those products and paint them through the different machines in the game, and lastly deliver these products.
Points (Budget) is added if the delivered product matches any of the orders.
#
# Code Structure
### Data/Miscellaneous
* **EPlayerProductState Enum**: The current state of the player regarding a product.
* **EProductTypes Enum**: Types of products.
* **EColors Enum**: Supported painting colors.
* **FOrder Struct**: Hold a product type and color.
* **FProduct Struct**: Hold a product type and a Mesh.
### Main CA Classes
* **BP_CACharacter**:
  - The character is only responsible for movement and firing an "Interact" event on the server, which traces a sphere that calls an interact function on any hit actor the implements **BPI_Interactable**.
* **BP_CAPlayerController**: Handles input and UI (client).
* **BP_CAPlayerState**: Handles all player-related replicated values, like the player's state.
* **BP_CAGameState**:
  - Handles all game requirements that are shared across all players, like the budget and orders.
  - Includes a handful of utility and helper functions that are used in other blueprints.
### Interactables
* **BPI_Interactable**: A simple interface with one "Interact" function.
* **BP_InteractableActorBase**: Base class for all intractable actors. Implements BPI_Interactable.
* **BP_Product**:
  - When interacted with, gets attached to the player.
  - Can dynamically change its color.
* **BP_RequestMachine**: When interacted with, creates the products list widget for the player.
* **BP_CarvingMachine**:
  - When interacted with, Spawns a product of the type the player's selected.
  - Spawns up to a maximum number at once. The number is decided in the GameState.
  - Spawns products with an offset based on their spot.
* **BP_PaintingWorkshop**:
  - When interacted with, places the product that the player is holding and prepares it for painting.
  - If the player had already placed it, it returns the product to them.
* **BP_PaintCan**: When interacted with, changes the color of the product on the painting workshop to match the color of the can.
* **BP_DeliveryStation**: When interacted with, triggers a check for the order on the game state that handles score and removal of any existing matching orders.
* ### Widgets
* **WBP_HUD**: Main player widget. Has the following:
  - Budget text label.
  - List of **WBP_Order**.
* **WBP_ProductSelection**: Contains a list of **WBP_Button**, one for each product type in the game.
### Other
* Showcase level: fully functional level with text renderers for clarity.
* Static Meshes: Simple models created in Blender that are assigned to products.
