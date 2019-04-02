# Setup of the filament

In this chapter, the basic setup of the filament is introduced.

## - Basic framework of filament in your application

When integrating the filament in a application, `Engine`, `Renderer`, `View`, `Camera` and `Scene` are basically needed.


### - `Engine`

As introduced in the `Engine.h`, the `Engine` instance keeps track of all resources created by the user and manage the rendering thread as well as the hardware render.
> An Engine instance main function is to keep track of all resources created by the user and manage the rendering thread as well as the hardware renderer.

> To use filament, an Engine instance must be created first:
```
#include <filament/Engine.h>
using namespace filament;

Engine* engine = Engine::create();
```


### - `Render`


From `Renderer.h`:
> A Renderer instance represents an operating system's window.

> Typically, applications create a Renderer per window. The Renderer generates drawing commands for the render thread and manages frame latency.

> A Renderer generates drawing commands from a View, itself containing a Scene description.









---

### - Sample

> A typical filament render loop looks like this:
```
#include <filament/Engine.h>
#include <filament/Renderer.h>
#include <filament/Scene.h>
#include <filament/View.h>
using namespace filament;

Engine* engine       = Engine::create();
SwapChain* swapChain = engine->createSwapChain(nativeWindow);
Renderer* renderer   = engine->createRenderer();
Scene* scene         = engine->createScene();
View* view           = engine->createView();

view->setScene(scene);

do {
     // typically we wait for VSYNC and user input events
    if (renderer->beginFrame(swapChain)) {
         renderer->render(view);
         renderer->endFrame();
     }
} while (!quit);

engine->destroy(&view);
ngine->destroy(&scene);
engine->destroy(&renderer);
engine->destroy(&swapChain);
Engine::destroy(&engine); // clears engine*
```
