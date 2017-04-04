# solarized-console
A port of the [Solarized](http://ethanschoonover.com/solarized) color scheme for Windows consoles

The default color schemes for the Windows Command shell and PowerShell are both eye-bleedingly dreadful. I like the idea and look of the Solarized color scheme, but existing ports had problems that bothered me. For an example, see [this port](https://github.com/neilpa/cmd-colors-solarized) which puts subtly different shades of black and white into slots with names/meanings like "Green", "Yellow", "Blue", and "Aqua". This causes compatibility problems with other programs that use the colors in these slots expecting to get a Green/Yellow/etc, sometimes resulting in illegible text unless some kind of fix is applied, as the referenced project does for PSReadLine. However, other programs such as NPM remain stuck with broken-looking colors.

The fundamental problem is that Solarized is a 16-color scheme that dedicates fully 8 of its colors to foreground and background colors, some of which are only subtly different. Meanwhile, the Windows Command and PowerShell color palettes have names assigned to them that do not align well with this. If you try to shoehorn all 16 Solarized colors into the Windows console color scheme, you will end up with some of those 8 foreground/background colors inhabiting spots meant for contrasting colors. While browsing over the main Solarized page, I noticed that the colors are designed to be scaled down to smaller palettes. So I thought, why not choose only the main FG/BG colors for the light and dark color schemes and fill the remaining slots with the closest matching Solarized color? This maintains a high degree of compatibility with the conventions established by the names of the Windows console colors while preserving the integrity of the Solarized palette.

## Colors

There are 16 colors in the Windows console. I chose to use 4 for the primary Solarized light/dark fore/background, leaving 12 remaining colors to assign. Solarized provides only 8 colors, so some colors must be repeated. One could choose a variety of strategies to try to minimize the chance of programs using the same Solarized color for foreground and background; this is merely one possible configuration.

<table>
	<tr>
		<th>ColorTable Index</th>
		<th>Command/PowerShell Color</th>
		<th>Solarized Color</th>
		<th>Hex</th>
		<th>RGB</th>
	</tr>
	<tr>
		<td>00</td>
		<td>Black/Black</td>
		<td>base03 (Dark BG)</td>
		<td>#002b36</td>
		<td>  0  43  54</td>
    </tr>
	<tr>
		<td>01</td>
		<td>Blue/DarkBlue</td>
		<td>Blue</td>
		<td>#268bd2</td>
		<td> 38 139 210</td>
	</tr>
    <tr>
		<td>02</td>
		<td>Green/DarkGreen</td>
		<td>Green</td>
		<td>#859900</td>
		<td>133 153   0</td>
	</tr>
    <tr>
		<td>03</td>
		<td>Aqua/DarkCyan</td>
		<td>Cyan</td>
		<td>#2aa198</td>
		<td> 42 161 152</td>
	</tr>
	<tr>
		<td>04</td>
		<td>Red/DarkRed</td>
		<td>Red</td>
		<td>#dc322f</td>
		<td>220  50  47</td>
	</tr>
    <tr>
		<td>05</td>
		<td>Purple/DarkMagenta</td>
		<td>Violet</td>
		<td>#6c71c4</td>
		<td>108 113 196</td>
	</tr>
    <tr>
		<td>06</td>
		<td>Yellow/DarkYellow</td>
		<td>Orange</td>
		<td>#cb4b16</td>
		<td>203  75  22</td>
	</tr>
    <tr>
		<td>07</td>
		<td>White/Gray</td>
		<td>base0 (Dark FG)</td>
		<td>#839496</td>
		<td>131 148 150</td>
	</tr>
    <tr>
		<td>08</td>
		<td>Gray/DarkGray</td>
		<td>base00 (Light FG)</td>
		<td>#657b83</td>
		<td>101 123 131</td>
	</tr>
    <tr>
		<td>09</td>
		<td>LightBlue/Blue</td>
		<td>Blue</td>
		<td>#268bd2</td>
		<td> 38 139 210</td>
	</tr>
    <tr>
		<td>10</td>
		<td>LightGreen/Green</td>
		<td>Green</td>
		<td>#859900</td>
		<td>133 153   0</td>
	</tr>
    <tr>
		<td>11</td>
		<td>LightAqua/Cyan</td>
		<td>Cyan</td>
		<td>#2aa198</td>
		<td> 42 161 152</td>
	</tr>
    <tr>
		<td>12</td>
		<td>LightRed/Red</td>
		<td>Red</td>
		<td>#dc322f</td>
		<td>220  50  47</td>
	</tr>
    <tr>
		<td>13</td>
		<td>LightPurple/Magenta</td>
		<td>Magenta</td>
		<td>#d33682</td>
		<td>211  54 130</td>
	</tr>
    <tr>
		<td>14</td>
		<td>LightYellow/Yellow</td>
		<td>Yellow</td>
		<td>#b58900</td>
		<td>181 137   0</td>
	</tr>
    <tr>
			<td>15</td>
		<td>BrightWhite/White</td>
		<td>base3 (Light BG)</td>
		<td>#fdf6e3</td>
		<td>253 246 227</td>
    </tr>
</table>

Dark BG/FG are at 00/07; Light BG/FG are at 15/08.

## Installation

From what I can find on the internet, Windows console settings work something like this: Defaults are stored in the registry, and the first time a console (Command or PowerShell) shortcut is run, the defaults are copied to the shortcut. Thereafter, the shortcut's settings are used. Unfortunately, I have not found a good way to script setting the colors of a shortcut once they've been set, so some manual effort may be involved.

### Setting default console colors

Back up your own `HKEY_CURRENT_USER\Console` registry settings first if you want to be able to revert at a later time, then merge `console-solarized-12-color.reg` into your registry.

### Setting console colors manually

Run the console whose colors you wish to change, then right-click on the window border and click Properties. Click the Colors tab and do the following for each color in the list:

1. Left-click the color in the list
2. Manually type in the RGB values for the color table
3. Tab out of the last (Blue) box. If you do not tab out before clicking the next color, the last value will not get saved.
4. GOTO 1

Once all the colors are input, set the Screen Text/Background and Popup Text/Background as desired. For Solarized Dark, use color table 00/07 for Screen Text/Background and 15/08 for Popup Text/Background. For Solarized Light, use 15/08 for Screen and 00/07 for Popup.

The main Solarized repository is on [GitHub](https://github.com/altercation/ethanschoonover.com/tree/master/projects/solarized).
