# 🎥 Loom Scraper - Videos & Folders

![https://apify.com/dz_omar/loom-video-scraper](https://raw.githubusercontent.com/DZ-ABDLHAKIM/loom-scrape-pro/refs/heads/main/Screenshot%20of%20Loom%20interface%20with%20scraper%20workflow%20visualization.png)

Transform your **Loom videos into searchable, downloadable archives** with complete metadata, transcripts, and comments across individual videos and entire folders.

Perfect for **content creators**, **educators**, and **businesses** who need to archive, analyze, or repurpose their Loom content without coding complexity.

---

## 🚀 Key Benefits & Use Cases

### **📚 For Educators & Trainers**
- Archive online courses and tutorial libraries with searchable transcript databases
- Backup training materials before expiration and generate study notes automatically
- Create comprehensive knowledge bases from video content

### **💼 For Business Teams**
- Archive team presentations, meeting recordings, and video communications
- Generate meeting transcripts for documentation and compliance
- Build searchable knowledge databases from organizational video content

### **🎯 For Content Creators**
- Bulk download and organize video libraries with rich metadata
- Create searchable video databases with full transcript capabilities
- Repurpose content across platforms efficiently

---

## 🔎 Complete Data Extraction

### 📹 **Video Intelligence**
- **Metadata**: ID, title, description, thumbnails, creation date, duration, quality
- **Engagement**: Views, reactions, comments count and full comment threads
- **Technical**: File format, direct download URLs, sharing links
- **Creator**: Owner information, avatars, profile data

### 📝 **Transcript Processing**
- **Multiple Formats**: SRT, VTT, TXT, XML exports with precise timestamps
- **Clean Text**: Formatted, readable content ready for analysis
- **Search Ready**: Full-text search capabilities across your library
- **Integration**: Compatible with video players and analysis tools

### 📂 **Folder Operations**
- **Bulk Processing**: Handle entire folders automatically with progress tracking
- **Mixed Operations**: Combine individual videos and folders in one request
- **Batch Reports**: Summary statistics and completion status for each folder

---

## ⚠️ Important: Account Videos vs Individual URLs

### **Account Videos Processing** (`includeAccountVideos: true`)
- Processes **all videos from your Loom account**
- Supports date filtering (`startDate`, `endDate`)
- Supports custom sorting (`videoSortOrder`)
- Requires authentication (email/password or cookies)

### **Individual URL Processing** (default behavior)
- Processes **only the specific URLs you provide**
- Date filters and sort order are **ignored**
- Works with or without authentication
- Processes videos in the order you list them

---

## ⚙️ Configuration Options

### 🔗 **Input URLs**
Process individual videos, entire folders, or mixed content:

```json
{
  "url": [
    "https://www.loom.com/share/08163614158646f7aa21e53997cd58e8",
    "https://www.loom.com/share/folder/abc123def456"
  ]
}
```

### 📥 **Download Options**

#### 🎞️ `downloadVideo` (Boolean)
- **Default**: `false`
- **Format**: Original MP4 quality preserved
- **Use Case**: Full video archiving and offline access
- **Note**: ✅ **Works even when owner has disabled downloads** in video settings

#### 📝 `downloadTranscript` (Boolean)
- **Default**: `false`
- **Integration**: Ready for video players and analysis tools

#### 📄 `outputFormat` (String)
- **Default**: `"srt"`
- **Options**: 
  - `"srt"`: Standard subtitle format (most compatible)
  - `"vtt"`: Web-friendly with CSS styling support
  - `"txt"`: Clean text without timestamps
  - `"xml"`: Full metadata structure

### 🔐 **Account Videos Options** (Only when `includeAccountVideos` is enabled)

These parameters only work when scraping your own Loom account videos. They have no effect when processing individual video URLs or public folders.

#### 📅 `startDate` (String)
- **Default**: `"2016-01-01"`
- **Format**: `"YYYY-MM-DD"`
- **Purpose**: Filter videos by earliest upload date to include from your account
- **⚠️ Note**: Only applies to your own account videos, not individual URLs

#### 📅 `endDate` (String)
- **Default**: `"2030-12-31"`
- **Format**: `"YYYY-MM-DD"`
- **Purpose**: Filter videos by latest upload date to include from your account
- **⚠️ Note**: Only applies to your own account videos, not individual URLs

#### 📅 `videoSortOrder` (String)
- **Default**: `"ASC"`
- **Options**: 
  - `"ASC"`: Oldest to Newest - Shows the earliest videos first
  - `"DESC"`: Newest to Oldest - Shows the most recently uploaded videos first
- **⚠️ Note**: Only applies when processing your own account videos, not individual URLs or folders

---

## ⚠️ Important: Memory Requirements for Video Downloads

When `downloadVideo` is enabled, the Actor requires significantly more memory. **Insufficient memory will cause failures** with OOM (Out Of Memory) errors.

### ✅ Recommended Memory Settings:

| Use Case | Memory Required |
|----------|----------------|
| Metadata/transcripts only | 512MB-1024MB |
| 1-5 video downloads | 1024MB |
| Large folders/bulk downloads | 2048MB or more |

Set memory in your run configuration: 2 GB or more

### 💡 Performance Tips:
- Process videos sequentially, not in parallel
- Split large folders into smaller batches
- Monitor usage from the Apify Console

### 📖 **[Learn more about Apify usage and resources](https://docs.apify.com/platform/actors/running/usage-and-resources)**
---

## 🔐 Authentication & Private Content Access

The Actor supports **scraping your private Loom videos** - perfect for backing up private workspaces or archiving internal content that isn't publicly shared.

### **Authentication Methods** (in priority order):

#### ✅ **Method 1: Email + Password** (Recommended)
```json
{
  "email": "your-email@example.com",
  "password": "your-password"
}
```
- Automatic login with fresh session
- Access to all private videos in your account
- Secure credential handling (encrypted and cleared after use)

#### 🍪 **Method 2: Browser Cookies** (Fallback)
```json
{
  "customCookies": [
    {
      "name": "connect.sid",
      "value": "s%3A123abc...",
      "domain": ".loom.com",
      "path": "/",
      "secure": true,
      "httpOnly": true
    }
  ]
}
```


### **Getting Browser Cookies**

1. **Install Extension**:

<table>
  <tr>
    <td align="center">
      <strong>
        <a href="https://cookie-editor.com/" target="_blank" rel="noopener noreferrer">🍪 Cookie-Editor Extension</a>
      </strong>
    </td>
    <td align="center">
      <strong>
        <a href="https://chromewebstore.google.com/detail/copy-cookies/jcbpglbplpblnagieibnemmkiamekcdg" target="_blank" rel="noopener noreferrer">📋 Copy Cookies Extension</a>
      </strong>
    </td>
  </tr>
  <tr>
    <td>
      <img src="https://raw.githubusercontent.com/DZ-ABDLHAKIM/loom-scrape-pro/refs/heads/main/add_Cookie_Editor.gif" width="100%">
    </td>
    <td>
      <img src="https://raw.githubusercontent.com/DZ-ABDLHAKIM/loom-scrape-pro/refs/heads/main/add_Copy_Cookies.gif" width="100%">
    </td>
  </tr>
</table>


2. **Export Process**:
   - Navigate to loom.com and log in
   - Use extension to export cookies as JSON
   - Paste into `customCookies` parameter

3. **Authentication Priority**:
   - **Email + Password** → Fresh login (highest priority)
   - **Custom Cookies** → Fallback method
   - **No Auth** → Public content only

---


Process:
1. Navigate to loom.com and log in
2. Use extension to export cookies as JSON
3. Paste into `customCookies` parameter

**Note**: Without authentication, only public content can be accessed.

---

## 📊 Sample Output Structure

![Sample Output](https://raw.githubusercontent.com/DZ-ABDLHAKIM/loom-scrape-pro/refs/heads/main/Sample_Output.png)

```json
{
  "video": {
    "id": "388fe9c5db854403bceefe52ea85dede",
    "title": "How to Use YouTube Scraper Effectively 🚀",
    "url": "https://www.loom.com/share/388fe9c5db854403bceefe52ea85dede",
    "thumbnails": "https://cdn.loom.com/sessions/thumbnails/...",
    "created_at": "2025-07-11T09:47:40.065Z",
    "duration_seconds": 38.28,
    "views": 0,
    "reactions": 7,
    "comments_count": 6,
    "owner": "TECH FRIDAY",
    "avatars": "https://cdn.loom.com/avatars/...",
    "download": {
      "available": true,
      "url": "https://api.apify.com/v2/key-value-stores/.../video.mp4",
      "format": "mp4"
    }
  },
  "transcript": {
    "text": "How to use, uhm, YouTube Scraper. First, we will...",
    "download": {
      "format": "SRT",
      "url": "https://api.apify.com/v2/key-value-stores/.../transcript.srt",
      "available": true
    }
  },
  "comments": [
    {
      "id": "100664080",
      "username": "Mohamad Abdlrahman",
      "content": "tyfgh",
      "created_at": "2025-07-11T10:58:55.610Z"
    }
  ]
}
```

---

## 🎯 Configuration Examples

### **Basic Video Archive**
```json
{
  "url": [
    "https://www.loom.com/share/08163614158646f7aa21e53997cd58e8"
  ],
  "downloadTranscript": true,
  "outputFormat": "srt"
}
```

### **Complete Folder Backup**
```json
{
  "url": [
    "https://www.loom.com/share/folder/abc123def456"
  ],
  "downloadVideo": true,
  "downloadTranscript": true,
  "outputFormat": "srt",
  "email": "your-email@example.com",
  "password": "your-password"
}
```
Set memory in your run configuration: 2 GB or more

### **Account Videos with Date Filter & Sort**
```json
{
  "includeAccountVideos": true,
  "downloadTranscript": true,
  "outputFormat": "srt",
  "startDate": "2024-01-01",
  "endDate": "2024-12-31",
  "videoSortOrder": "DESC",
  "email": "your-email@example.com",
  "password": "your-password"
}
```

### **Mixed Content: URLs + Account Videos**
```json
{
  "url": [
    "https://www.loom.com/share/08163614158646f7aa21e53997cd58e8",
    "https://www.loom.com/share/folder/abc123def456"
  ],
  "includeAccountVideos": true,
  "downloadVideo": false,
  "downloadTranscript": true,
  "outputFormat": "vtt",
  "startDate": "2024-06-01",
  "videoSortOrder": "DESC"
}
```

---

## 🔄 Advanced Features

### **Reliability & Performance**
- **State Management**: Auto-resume from interruption points with progress tracking
- **Error Handling**: Robust recovery with automatic retry mechanisms
- **Storage Optimization**: Efficient file organization with direct download URLs
- **Detailed Logging**: Complete processing history and performance monitoring

### **Content Processing**
- **Platform Updates**: Migration support for Loom platform changes
- **Batch Operations**: Efficient bulk processing with folder progress tracking
- **Multiple Formats**: Structured file naming and organized output

---

## 🛠️ Troubleshooting

### **Authentication Issues**
- **Verify credentials**: Check email/password accuracy
- **Update cookies**: Ensure browser cookies are current
- **Try fallback**: Use alternative authentication method

### **Missing Content**
- **Transcripts**: Must be enabled by video owner (Settings → Audience → Transcript → Toggle ON)
- **Private videos**: Requires valid authentication
- **Permissions**: Verify sharing permissions with content creator

### **Performance Issues**
- **Memory errors**: Increase memory allocation for video downloads
- **Large folders**: Split into smaller batches
- **Slow processing**: Check network connection and Loom server status

---

## 🤝 Support & Resources

### **Getting Help**
- **📧 Email**: [fridaytechnolog@gmail.com](mailto:fridaytechnolog@gmail.com)
- **🐙 GitHub**: [DZ-ABDLHAKIM](https://github.com/DZ-ABDLHAKIM)
- **🐦 Twitter**: [@DZ_45Omar](https://x.com/DZ_45Omar)
- **🔧 Apify**: [dz_omar](https://apify.com/dz_omar)

### **Legal & Compliance**
- **Responsible Usage**: Only scrapes publicly accessible data with proper rate limiting
- **Terms Compliance**: Follows Loom's terms of service without bypassing security
- **Data Protection**: Encrypted credential handling with automatic cleanup
- **Privacy Respect**: No unauthorized data collection with transparent usage policies

---

**Version**: 2.x  
**Last Updated**: July 2025  
**Status**: Active Development
