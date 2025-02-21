# Creating a Custom Icon Pack for Linux

Welcome to the guide for developing your own custom icon pack for Linux graphical environments. This brief article will provide detailed instructions and practical examples to help you create and implement a custom icon theme.

## Icon Locations on the System

First, it is important to explain where icons are usually stored. There are many possible directories to store icon files, but the most common ones are:

- **User Icons** (`~/.icons/`): Icons stored here are only accessible by the current user.
- **System Icons** (`/usr/share/icons/`): Icons in this directory are available to all system users.
- **Application Icons** (`/usr/share/pixmaps/`): Contains icons used by various applications and software packages.

> [!NOTE]  
> Applications typically look for icons first in `~/.icons/`, then in `/usr/share/icons/`, and finally in `/usr/share/pixmaps/`.

## Creating a Directory for Your Custom Theme

Now that we've covered some of the directories, it's important to select one to start creating your icons. You can choose between the following:

- For personal use: `~/.icons/`
- For global use: `/usr/share/icons/`

Simply navigate to the chosen directory through the terminal or graphical environment and create a folder with your icon theme's name. For example, via the terminal, it would look something like this:

```bash
mkdir -p ~/.icons/YourThemeName
```

> [!IMPORTANT]  
> Replace `YourThemeName` with the desired name for your theme.

## Directory Structure of the Icon Pack

Inside your theme's directory, you need to organize the icons into categorized subdirectories. The most common structure is:

```txt
YourThemeName/
├── 16x16/
├── 22x22/
├── 24x24/
├── 32x32/
├── 48x48/
├── 64x64/
├── 128x128/
├── 256x256/
├── scalable/
├── cursors/
└── index.theme
```

Each directory (except for `cursors` and `index.theme`) represents the icon size in pixels. Inside these directories, the icons are organized into categories such as:

- `actions`: Actions (e.g., save, open);
- `apps`: Applications;
- `devices`: Devices;
- `places`: Places (e.g., folders, directories);
- `mimetypes`: File types;
- `status`: Status and notifications.

For example, the structure for 48x48 pixel icons would look like this:

```txt
YourThemeName/48x48/
├── actions/
├── apps/
├── devices/
├── places/
├── mimetypes/
└── status/
```

> [!IMPORTANT]  
> You can also structure your icon pack by first using the category names and then allocating the different sizes within these directories. Feel free to do whatever suits you best!

## The `index.theme` File

The `index.theme` file is essential for your icon theme. It serves as an index that defines the theme's properties and guides the system in locating the icons. Here’s a basic example of `index.theme`:

```ini
[Icon Theme]
Name=YourThemeName
Comment=Description of your icon theme
Example=folder

[Directories]
16x16/actions
16x16/apps
16x16/devices
16x16/places
16x16/mimetypes
16x16/status

# Repeat for other sizes and categories

[16x16/actions]
Size=16
Context=Actions
Type=Fixed

[16x16/apps]
Size=16
Context=Applications
Type=Fixed

# Continue for the other directories
```

### Explanation of Sections

- `[Icon Theme]`: General information about the theme.
  - `Name`: The name of the theme.
  - `Comment`: A brief description.
  - `Example`: A representative icon name from the theme.

- `[Directories]`: List of directories included in the theme.

- `[16x16/actions]`: Specific settings for each directory.
  - `Size`: The size of the icons in the directory.
  - `Context`: The context or category of the icons.
  - `Type`: Icon type (`Fixed` for fixed sizes, `Scalable` for resizable SVGs).

For more details about the `index.theme` file, refer to the [Freedesktop Icon Theme Specification](https://specifications.freedesktop.org/icon-theme-spec/icon-theme-spec-latest.html).

## Supported File Formats

The commonly used file formats for icons in Linux are:

- **SVG**: Scalable vector graphics, ideal for icons that need to be resized without losing quality.
- **PNG**: Raster images, suitable for fixed-size icons.

> [!TIP]  
> Other formats, like **XPM**, are also supported but are less common.

## Creating a Custom Icon

Let's create a custom application icon:

1. **Choose the Size and Category**:
    - Suppose we want to create a 64x64 pixel icon for an application.
    - The corresponding directory would be `YourThemeName/64x64/apps/`.

2. **Create the Directory if It Doesn't Exist**:

   ```bash
   mkdir -p ~/.icons/YourThemeName/64x64/apps/
   ```

3. **Create the Icon**:
   - Use your preferred graphic editor (like [Inkscape](https://inkscape.org/)) to create the icon in the desired dimensions.
   - Save the file in PNG or SVG format.

4. **Name the File Correctly**:
   - The file name should follow the [Icon Naming Specification](https://specifications.freedesktop.org/icon-naming-spec/icon-naming-spec-latest.html).
   - For example, for a text editor, the name could be `accessories-text-editor.png`.

5. **Save the Icon in the Appropriate Directory**:
   - Place the file in `~/.icons/YourThemeName/64x64/apps/`.

## Useful Tools for Creating Icons

To simplify the creation process, consider using tools such as:

- **[Ikona](https://apps.kde.org/ikona/)**: An application dedicated to icon design, available for Linux.

> **Install Ikona via Flatpak**:
>
> ```bash
> flatpak install flathub org.kde.Ikona
> flatpak run org.kde.Ikona
> ```

## Applying the Icon Theme

After creating your icon set, you need to apply it to your desktop environment:

- **GNOME**:
  - Install the *GNOME Tweaks* application if you don’t have it yet:

    ```bash
    sudo apt install gnome-tweaks   # Debian/Ubuntu
    sudo dnf install gnome-tweaks   # Fedora
    ```

  - Open *GNOME Tweaks*, go to "Appearance" and select your icon theme.

- **KDE Plasma**:
  - Go to *System Settings* > *Appearance* > *Icons* and choose the theme.

- **XFCE**:
  - Go to *Settings* > *Appearance* > *Icons* and select your theme.

- **LXQt**:
  - Go to *System Preferences* > *Appearance* > *Icon Theme*.

If the theme doesn’t appear immediately, try running this command to update the icon cache:

```bash
gtk-update-icon-cache -f ~/.icons/YourThemeName
```

If the theme is in the `/usr/share/icons/` folder, use:

```bash
sudo gtk-update-icon-cache -f /usr/share/icons/YourThemeName
```

## Resources and Templates to Get Started

To help you get started, here are some useful templates:

- **[Base for Creating an Icon Theme](https://github.com/snwh/paper-icon-theme)** (Example of the Paper theme)
- **[`index.theme` File Template](https://specifications.freedesktop.org/icon-theme-spec/icon-theme-spec-latest.html#example)** (Official Freedesktop documentation)
- **[Papirus Icon Set for Reference](https://github.com/PapirusDevelopmentTeam/papirus-icon-theme)**

## Publishing Your Icon Pack

Once you’ve created and tested your custom icon pack, you can share it with the community. Here are some popular platforms where you can publish your work:

### 1. Opendesktop.org

[Opendesktop.org](https://www.opendesktop.org/) is a popular platform for sharing themes, icons, and other Linux-related resources.

### 2. GitHub

[GitHub](https://github.com/) is a widely used code hosting platform that’s ideal for developers who want to share their projects and collaborate with others.

### 3. Pling.com

[Pling.com](https://www.pling.com/) is a platform that hosts a variety of content, including themes and icons for Linux.

### 4. DeviantArt

[DeviantArt](https://www.deviantart.com/) is an online art community where many designers share their Linux themes and icons.

## Conclusion

Creating a custom icon theme on Linux may seem challenging at first, but with this guide, you have all the basics to get started. From organizing directories to setting up the `index.theme` file, each step is crucial to ensuring a functional and stylish package.

If you have questions or want to share your progress, feel free to explore forums like [r/unixporn](https://www.reddit.com/r/unixporn/) on Reddit or the theme groups on [Pling](https://www.pling.com/).

We hope this guide has been helpful!
