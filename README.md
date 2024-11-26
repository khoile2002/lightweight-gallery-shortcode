# lightweight-gallery-shortcode
lightweight Hugo gallery shortcode for Hinode theme and Hugo bootstrap 5 theme
- Only pages with shortcodes will load CSS and JS
- use modal Bootstrap
- minimal JS

To install and use the Hugo gallery shortcode  follow these steps:

### **1. Create the Required Folder Structure**

1. create the following folder and file structure:
   ```
   ├── assets/
   │   ├── img/
   │   │   ├── <album-folder>/  # Folder containing images
   │   │   │   ├── image1.jpg
   │   │   │   ├── image2.png
   │   │   │   ├── album.txt  # Optional metadata
   │   ├── scss/
   │   │   ├── components/
   │   │   │   ├── _gallery.scss
   │   ├── js/
   │       ├── gallery.js
   ├── layouts/
   │   ├── shortcodes/
   │   │   ├── gallery.html
   ```

2. Copy the provided files into the respective locations:
   - `gallery.html` → `layouts/shortcodes/gallery.html`
   - `_gallery.scss` → `assets/scss/components/_gallery.scss`
   - `gallery.js` → `assets/js/gallery.js`

---

---

### **3. Add Images and Metadata**

1. **Add Images**:
   - Place your images in the folder `assets/img/<album-folder>/`.
   - Supported formats: `.jpg`, `.jpeg`, `.png`, `.webp`. you can add more formats
   - {{ $thumbnail := $imageResource.Resize "400x267 webp" }} => change the size of thumbnail you want                                           
   -  {{ $original := $imageResource.Resize "800x webp" }} change the size of popup image like 840, 920....                                                                
                
2. **Add Metadata** (optional):
   - Create an `album.txt` file in the same folder as the images. Each line represents metadata for one image, in the format:
     ```
     Title 1|Caption 1
     Title 2|Caption 2
     ```

---

### **4. Use the Shortcode in a Post**

1. **Invoke the Shortcode in a Markdown File**:
   In your content file (e.g., `content/posts/gallery-example.md`), use the shortcode as follows:
   ```markdown
   {{< gallery "album-folder" 3 >}}
   ```
   - `"album-folder"`: The folder name containing the images (e.g., `travel-album`).
   - `3`: Number of columns to display per row (from 1 to 3 defaults to 2 if not provided).

## Features
### 1. **Automatic Image Resource Handling**
- Automatically reads image files from the specified folder (`assets/img/`) and generates appropriately sized images:
  - Thumbnail: 400x267 webp (compact, optimized for fast display).
  - Original image: 800px width webp (higher quality for zooming when needed).

### 2. **Support for Custom Metadata**
- Integrates the ability to read metadata (title, caption) from an `album.txt` file, making it easy to manage image descriptions without directly editing the source code.

### 3. **Interactive Image Display**
- Uses Bootstrap modals to display larger images upon clicking:
  - Detailed information (title, caption) is presented clearly and concisely.
  - Users can easily close the modal with a button or by clicking outside the modal.

### 4. **High Customizability**
- Input variables (`.Get`) allow for defining:
  - The directory path containing the images.
  - The number of columns displayed (flexible interface customization).

### 5. **High Performance and SEO Optimization**
- Images use lazy-loading (`loading="lazy"`) to improve page loading speed, especially on mobile devices.
- Images are in webp format, reducing file size while maintaining quality.

### 6. **Simple and Efficient JavaScript**
- Lightweight script that only triggers when the user opens the modal, avoiding delays on the main page.
- Data (title, caption) is retrieved directly from HTML attributes (`data-*`), minimizing reloads or API calls.

### 7. **Friendly Notification for Invalid Albums**
- Displays a user-friendly message if the image folder is empty or contains no valid files, enhancing user experience.
