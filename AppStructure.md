`concept`
# App Structure
Program structure:
```py
    # Simple Apps
    app-name-folder
        |
        +-- main.cpp
        +-- manifest.json
    
    # Complex Apps(containing libs)
    app-name-folder
        |
        +-- libs.cpp
        +-- libs.h
        +-- app
        |    |
        |    +-- main.cpp
        |    +-- manifest.json
        |
        +-- manifest.json
```
## Simple Apps
    These are apps having a small pourpouse(for dialoge's/small window).
## Complex Apps
    These are apps having much complex tasks and use libs(for file manager/media player).
### Simple App creation
- #### Requirements
    1. manifest.json
        ```json
        {
        "$schema": "https://schemas.cute.engineering/stable/cutekit.manifest.component.v1",
        "id": "hideo-app_name",
        "type": "exe",
        "description": "app_description",
        "requires": [
            "karm-ui",
            "karm-main"
            "additional_requirements"
        ]
        }
        ```
        The OS identify this file as the definition of your app.
    2. #### main.cpp
        ```cpp

        #include <karm-main/main.h>
        #include <karm-ui/app.h>
        #include <karm-ui/scafold.h>

        namespace app_namespace {

        Ui::Child app() {
            auto content = Ui::spacing(
                16,Ui::Empty()
            );

            return Ui::scafold({
                .icon = Mdi::app_icon,
                .title = "app_name",
                .titlebar = Ui::TitlebarStyle::DIALOG,
                .body = content,
                .size = {460, 360},
            });
            // when .titlebar has no value then its not a DIALOG
            // but now its a DIALOG(ie. no maximize and minimize button)
        }

        } // namespace app_namespace

        Res<> entryPoint(Ctx &ctx) {
            return Ui::runApp(ctx, app_namespace::app());
        }

        ```
- #### Dev Run
    ```shell
      unoptimized:
        $ ./skift.sh run hideo-app_name
      optimized:
        $ ./skift.sh run --target=:o3 hideo-app_name
    ```
