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
