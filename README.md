<p align="center"> <img src="https://upload.wikimedia.org/wikipedia/commons/5/5a/Animated_Wallpaper_Windows_10_-_Wallpaper_Engine.gif"></p>

## watermark_disabler
Disabling "Activate Windows" watermark made simple, the code in this repository is a PoC, and has not been tested above Windows 10 1803.

## how does this work?
The function responsible for drawing whole desktop including the watermark is xxxDesktopPaintCallback located in win32kfull.sys.
Both of the approaches used by this project were found while analyzing functions further down in the callstack.

### approach #1
As you can see from the snippets below, forcing gpsi->unk874h to be zero the checks will fail and the watermark won't be drawn.
```cpp
// global tagSERVERINFO* gpsi;
// global _THREADINFO* gptiCurrent;
if ( gpsi->unk874h != 0 )
{
	/* gptiCurrent + 0x1c0 = tagDESKTOP** */
	const auto desktop = gptiCurrent->desktops[1]; /* type: tagDESKTOP**, this is checked if it's grpdeskLogon, which is a global pointer to the lock screen */
	
	HWND desktop_window = nullptr;
	
	/* tagDESKTOP + 0xa8 = tagWnd* */
	if ( desktop )
		desktop_window = desktop->wnd; /* type: tagWnd*, I believe this is a pointer to the lock window? */
	
	should_draw_watermark = ( desktop_window == nullptr );
}

if ( should_draw_watermark )
	PaintWatermark(device_context, &desktop_rect);
```

### approach #2
PaintWatermark calls GreExtTextOutWInternal (which is the internal function for ExtTextOutW/NtGdiExtTextOutW in wingdi.h). 

The argument passed for size (c) is a global called "gSafeModeStrLen", by setting the size (c) to 0, the string won't be rendered. The pattern for the aforementioned global inside win32kfull is 44 8B C8 44 89 0D + 7


<p align="center"> <a href="https://www.buymeacoffee.com/tahiri" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/lato-orange.png" alt="Buy Me A Coffee" style="height: 51px !important;width: 217px !important;" ></a> <p>
<p align="center">
    <a href="https://yassertahiri.medium.com/">
    <img alt="Medium" src="https://img.shields.io/badge/Medium%20-%23000000.svg?&style=for-the-badge&logo=Medium&logoColor=white"/></a>
    <a href="https://twitter.com/THyasser1">
    <img alt="Twitter" src="https://img.shields.io/badge/Twitter%20-%231DA1F2.svg?&style=for-the-badge&logo=Twitter&logoColor=white"</a>
    <a href="https://discord.gg/crNvkTYPYG">
    <img alt="Discord" src="https://img.shields.io/badge/Discord%20-%237289DA.svg?&style=for-the-badge&logo=discord&logoColor=white"/></a>
</p>
