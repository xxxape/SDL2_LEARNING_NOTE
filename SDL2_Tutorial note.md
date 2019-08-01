# 目录
- [Lesson 01 Hello SDL](#lesson-01-hello-sdl)
- [Lesson 02 Getting an Image on the Screen](#lesson-02-getting-an-image-on-the-screen)
- [Lesson 03 Event Driven Programming](#lesson-03-event-driven-pProgramming)
- [Lesson 04 Key Presses](#lesson-04-key-presses)
- [Lesson 05 Optimized Surface Loading and Soft Stretching](#lesson-05-optimized-surface-loading-and-soft-stretching)
- [Lesson 06 Extension Libraries and Loading Other Image Formats](#lesson-06-extension-libraries-and-loading-other-image-formats)
- [Lesson 07 Texture Loading and Rendering](#lesson-07-texture-loading-and-rendering)
- [Lesson 08 Geometry Rendering](#lesson-08-geometry-rendering)
- [Lesson 09 The Viewport](#lesson-09-the-viewport)
- [Lesson 10 Color Key](#lesson-10-color-key)
- [Lesson 11 Clip Rendering and Sprite Sheets](#lesson-11-clip-rendering-and-sprite-sheets)
- [Lesson 12 Color Modulation](#lesson-12-color-modulation)
- [Lesson 13 Alpha Blending](#lesson-13-alpha-blending)
- []()
- []()


### Lesson 01 Hello SDL
SDL - a dynamically linked library

    -the header files(Library.h)
    -the library files(Library.lib)
    -the binary files(Library.dll)    
    
### Lesson 02 Getting an Image on the Screen
```
SDL_Init();  //Initializes SDL
SDL_Window* SDL_CreatWindow(const char* title,  //the title of the window
                            int         x,      //the x position of the window
                            int         y,      //the y position of the window
                            int         w,      //the width of the window
                            int         h,      //the height of the window
                            uint32      flags); //SDL_WindowFlags
                           
SDL_Surface* SDL_GetWindowSurface(SDL_Window* window);  //get the SDL surface associated with the window

SDL_Surface* SDL_LoadBMP(const char* file);     //the file containing a BMP image

SDL_FreeSurface(SDL_Surface* surface);

SDL_DestoryWindow(SDL_Window* window);

int SDL_BlitSurface(SDL_Surface*        src,        //to be copied from
                    const SDL_Rect*     srcrect,    //representing the rectangle to be
                    SDL_Surface*        dst,        //the blit target
                    SDL_Rect*           dstrect);   //representing the rectangle that is copied into
                    
int SDL_UpdateWindowSurface(SDL_Window* window);

SDL_Delay(milliseconds);
```

### Lesson 03 Event Driven Programming
```
int SDL_PollEvent(SDL_Event* event);
    event:the SDL_Event structure to be filled with the next event from the queue, or NULL.
```

### Lesson 04 Key Presses
```
structure: enum KeyPressSurface
{
    KEY_PRESS_SURFACE_DEFAULT,
    KEY_PRESS_SURFACE_UP,
    KEY_PRESS_SURFACE_DOWN,
    KEY_PRESS_SURFACE_LEFT,
    KEY_PRESS_SURFACE_RIGHT,
    KEY_PRESS_SURFACE_TOTAL
};
```

### Lesson 05 Optimized Surface Loading and Soft Stretching
```
SDL_Surface* SDL_ConverSurface(SDL_Surface*                 src,        //to convert
                                const SDL_PixelFormat*      fmt,        //be optimized for
                                uint32                      flags);

SDL_Rect
{
    int x,  //the x location of the rectangle's upper left corner
    int y,  //the y location of the rectangle's upper left corner
    int w,  //the width of the rectangle
    int h  //the height of the rectangle
}

int SDL_BlitScaled(SDL_Surface*         src,        //to be copied from
                    const SDL_Rect*     srcrect,
                    SDL_Surface*        dst,        //the blit target
                    SDLL_Rect*          dstrect);
```

### Lesson 06 Extension Libraries and Loading Other Image Formats
```
import SDL_image.h
int IMG_Init(int flags);
    flags:  IMG_INIT_JPG    0X01
            IMG_INIT_PNG    0X02
            IMG_INIT_TIF    0X04
```

### Lesson 07 Texture Loading and Rendering
```
SDL_Renderer ≈ SDL_Surface* gScreenSurface
SDL_texture  ≈ SDL_Surface* gHelloworld

SDL_bool SDL_SetHint(const char* name,
                     const char* value);
    SDL_SetHint(SDL_HINT_RENDER_SCALE.QUALITY, "1");
    
SDL_Renderer* SDL_CreateRenderer(SDL_Window*    window,
                                 int            index,
                                 uint32         flags);
    SDL_CreateRenderer(gWindow, -1, SDL_RENDERER_ACCELERATED);
    
int SDL_SetRenderDrawColor(SDL_Renderer*    renderer,
                           uint8            r,
                           uint8            g,
                           uint8            b,
                           uint8            a);

SDL_Texture* SDL_CreateTextureFromSurface(SDL_Renderer* renderer,
                                          SDL_Surface*  surface);

int SDL_RenderClear(SDL_Renderer* renderer)     //clear the current rendering target with the drawing color

int SDL_RenderCopy(SDL_Renderer*    renderer,
                   SDL_Texture*     texture,
                   const SDL_Rect*  srcrect,    //texture's size
                   const SDL_Rect*  dstrect);   //texture's position in renderer

void SDL_RenderPresent(SDL_Renderer* renderer); //undate the screen with any rendering performed since the previous call
```

### Lesson 08 Geometry Rendering
```
//fill a rectangle on the current rendering target with the drawing color
int SDL_RenderFillRect(SDL_Renderer* renderer,  //the rendering context
                        const SDL_Rect* rect);  //the rectangle to fill, or NULL for the entire rendering target 

//draw a rectangle on the current rendering target
int SDL_RenderDrawRect(SDL_Renderer* renderer,
                        const SDL_Rect* rect);

//draw a line on the current rendering target from (x1, y1) to (x2, y2)
int SDL_RenderDrawLine(SDL_Renderer* renderer,
                        int x1,
                        int y1,
                        int x2,
                        int y2);

//draw a point on the current rendering target
int SDL_RenderDrawPoint(SDL_Renderer* renderer,
                        int x,
                        int y);
```

### Lesson 09 The Viewport
```
//Top left corner viewport
SDL_Rect topletfView;
topleftView.x = 0;
topleftView.y = 0;
topleftView.w = SCREEN_WIDTH/2;
topleftView.h = SCREEN_HEIGHT/2;
int SDL_RenderSetViewPort(SDL_Renderer* renderer,
                          const SSDL_Rect* rect)    //set the drawing area
```

### Lesson 10 Color Key
```
Class LTexture{
    public:
        //Initializes variables
        LTexture();
        //Deallocates memory
        ~LTexture();
        //Loadimage at specified path
        bool loadFramFile(std::string path);
        //Deallocates texture
        void free();
        //Renders texture at given point
        void render(int x, int y)
        //Get image dimensions
        int getWidth();
        int getHeight();
    private:
        //The actual hardware texture
        SDL_Texture* mTexture;
        //Image dimensions
        int mWidth;
        int mHeight;
}

//set the color key(transparent pixel) in a surface
int SDL_SetColorKey(SDL_Surface* surface,
                    int flag,               //SDL_TRUE or SDL_FALSE
                    Uint32 key);

SDL_SetColorKey(loadedSurface, SDL_TRUE, SDL_MapRGB(loadedSurface -> format, 0, 0xff, 0xff);
```

### Lesson 11 Clip Rendering and Sprite Sheets
```
//把图片分成4个部分
SDL_Rect gSpriteClips[4]; 
//把clip大小的mTexture放在gRenderer的&renderQuad位置
SDL_RenderCopy(gRenderer, mTextire, clip, &renderQuad)
```

### Lesson 12 Color Modulation
```
SDL_SetTextureColorMod(SDL_Texture* texture,
                        Uint8 r,
                        Uint8 g,
                        Uint8 b);
//srcC = scrC × (color / 255)
```
例：原色(255, 255, 0)
    输入(255, 128, 255)
    得 (255, 128, 0)

### Lesson 13 Alpha Blending
```
//set the blend mode for a texture
int SDL_SetTextureBlendMode(SDL_Texture* texture,
                            SDL_BlendMode blendMode);
int SDL_SetTextureAlphaMod(SDL_Texture* texture,
                           Uint8 alpha);
//srcA = srcA × (alpha / 255)
```


111test
