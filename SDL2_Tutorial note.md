# Lesson 01 Hello SDL
SDL - a dynamically linked library

    -the header files(Library.h)
    -the library files(Library.lib)
    -the binary files(Library.dll)    
    
# Lesson 02 Getting an Image on the Screen
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

# Lesson 03 Event Driven Programming
```
int SDL_PollEvent(SDL_Event* event);
    event:the SDL_Event structure to be filled with the next event from the queue, or NULL.
```

# Lesson 04 Key Presses
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

# Lesson 05 Optimized Surface Loading and Soft Stretching
