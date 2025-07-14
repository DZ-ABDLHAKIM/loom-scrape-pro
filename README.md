# 🎥 Loom Scraper - Videos & Folders

![https://apify.com/dz_omar/loom-video-scraper](https://raw.githubusercontent.com/DZ-ABDLHAKIM/loom-scrape-pro/refs/heads/main/Screenshot%20of%20Loom%20interface%20with%20scraper%20workflow%20visualization.png)

Transform your **Loom videos into searchable, downloadable archives** with complete metadata, transcripts, and comments across individual videos and entire folders.

Perfect for **content creators**, **educators**, and **businesses** who need to archive, analyze, or repurpose their Loom content without coding complexity.

---

## 🚀 Why Use This Scraper?

### **📚 For Educators & Trainers**
- **Archive online courses** and tutorial libraries
- **Create searchable transcript databases** for student reference
- **Backup training materials** before they expire
- **Generate study notes** from video content automatically

### **💼 For Business Teams**
- **Archive team presentations** and meeting recordings
- **Create knowledge databases** from video communications
- **Backup important video assets** for compliance
- **Generate meeting transcripts** for documentation

### **🎯 For Content Creators**
- **Bulk download video libraries** for backup
- **Organize content catalogs** with rich metadata
- **Create searchable video databases** with transcript search
- **Repurpose video content** across platforms

---

## 🔎 What This Actor Extracts

### 📹 **Complete Video Intelligence**
- **📌 Video Metadata**: ID, title, description, thumbnails, creation date
- **📊 Engagement Data**: Views, reactions, comments count
- **⏱️ Technical Details**: Duration, quality, file format
- **👤 Creator Information**: Owner name, avatar, profile data
- **🔗 Direct Links**: Original Loom URLs and sharing links

### 📝 **Rich Transcript Data**
- **📄 Clean Text**: Formatted, readable transcript content
- **⏰ Timestamps**: Precise timing for every spoken word
- **📁 Multiple Formats**: SRT, VTT, TXT, and XML exports
- **🔍 Searchable Content**: Full-text search capabilities
- **💾 Download Ready**: Instant download URLs provided

### 💬 **Complete Comment Threads**
- **👥 User Information**: Commenter names and profiles
- **📅 Timestamps**: When each comment was posted
- **🧵 Thread Structure**: Organized comment hierarchies
- **📊 Engagement Metrics**: Comment counts and interactions

### 📂 **Folder Processing Power**
- **🎯 Bulk Operations**: Process entire folders automatically
- **📈 Progress Tracking**: Real-time folder completion status
- **🔄 Mixed Processing**: Combine folders and individual videos
- **📊 Batch Reports**: Summary statistics for each folder

---

## ⚙️ Smart Processing Options

### **Individual Videos**
Process single videos with complete data extraction:
```
https://www.loom.com/share/VIDEO_ID
```

### **Entire Folders**
Bulk process all videos in a folder:
```
https://www.loom.com/share/folder/FOLDER_ID
```

### **Mixed Operations**
Combine videos and folders in one request:
```json
[
  "https://www.loom.com/share/08163614158646f7aa21e53997cd58e8",
  "https://www.loom.com/share/folder/abc123def456"
]
```

---

## 🛠️ Configuration Options

### **Required Parameters**

#### `url` (Array)
List of Loom share URLs or video/folder IDs:

```json
{
  "url": [
    "https://www.loom.com/share/08163614158646f7aa21e53997cd58e8",
    "https://www.loom.com/share/folder/abc123def456"
  ]
}
```

### **Download Options**

#### `downloadVideo` (Boolean)
- **Default**: `false`
- **Storage Impact**: Video files consume significant space
- **Quality**: Original MP4 quality preserved
- **Use Case**: Full video archiving and offline access

#### `downloadTranscript` (Boolean)
- **Default**: `false`
- **Formats**: SRT, VTT, TXT, XML available
- **Integration**: Ready for video players and analysis tools
- **Search**: Enable full-text search across your library

#### `outputFormat` (String)
- **Default**: `"srt"`
- **Options**: 
  - **`"srt"`**: Standard subtitle format (most compatible)
  - **`"vtt"`**: Web-friendly with CSS styling support
  - **`"txt"`**: Clean text without timestamps
  - **`"xml"`**: Full metadata structure

### **Authentication Methods**

#### **Method 1: Email/Password** (Recommended)
```json
{
  "email": "your-email@example.com",
  "password": "your-password"
}
```
- ✅ **Highest Priority**: Automatic login with fresh session
- ✅ **Private Access**: Access private videos and folders
- ✅ **Security**: Credentials encrypted and cleared after use

#### **Method 2: Browser Cookies** (Fallback)
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

---

## 📊 Sample Output

*![Sample_Output-of-scrape-pro](https://raw.githubusercontent.com/DZ-ABDLHAKIM/loom-scrape-pro/refs/heads/main/Sample_Output.png)*

### **Complete Video Data Structure**
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

## 🎯 Quick Start Examples

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

### **Mixed Content Processing**
```json
{
  "url": [
    "https://www.loom.com/share/08163614158646f7aa21e53997cd58e8",
    "https://www.loom.com/share/folder/abc123def456"
    ],
  "downloadVideo": false,
  "downloadTranscript": true,
  "outputFormat": "vtt"
}
```

---

## 🔐 Authentication Guide

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

## 🔄 Advanced Features

### **State Management & Resumability**
- **✅ Auto-Resume**: Continues from interruption point
- **✅ Progress Tracking**: Real-time status updates
- **✅ Migration Support**: Handles platform updates
- **✅ Folder Progress**: Individual completion tracking

### **Error Handling & Reliability**
- **🛡️ Robust Recovery**: Automatic retry mechanisms
- **📊 Detailed Logging**: Complete processing history
- **🔄 Fallback Methods**: Multiple authentication options
- **📈 Performance Monitoring**: Real-time metrics

### **Storage & Downloads**
- **💾 Optimized Storage**: Efficient file organization
- **🔗 Direct URLs**: Instant download access
- **📁 Batch Processing**: Efficient bulk operations
- **🗂️ Organized Output**: Structured file naming

---

## 🛠️ Troubleshooting

### **Common Issues & Solutions**

#### **Authentication Failures**
- **✅ Check credentials**: Verify email/password accuracy
- **🔄 Try cookies**: Use browser cookie method as fallback
- **📅 Update cookies**: Ensure cookies are current

#### **Private Content Access**
- **🔑 Authentication**: Ensure proper account access
- **👥 Permissions**: Verify sharing permissions
- **⚙️ Settings**: Check creator's privacy settings

#### **Missing Transcripts**
- **📝 Creator Settings**: Transcripts must be enabled by video owner
- **🔧 Enable Path**: Settings → Audience → Transcript → Toggle ON
- **📞 Contact Creator**: Request transcript access

---

## 🤝 Support & Resources

### **Getting Help**
- **📧 Email**: [fridaytechnolog@gmail.com](mailto:fridaytechnolog@gmail.com)
- **🐙 GitHub**: [DZ-ABDLHAKIM](https://github.com/DZ-ABDLHAKIM)
- **🐦 Twitter**: [@DZ_45Omar](https://x.com/DZ_45Omar)
- **🔧 Apify**: [dz_omar](https://apify.com/dz_omar)

---

## 📜 Legal & Compliance

### **Responsible Usage**
- **✅ Public Content**: Only scrapes publicly accessible data
- **🤖 Rate Limiting**: Respects server load limitations
- **📋 Terms Compliance**: Follows Loom's terms of service
- **🔒 No Bypassing**: Doesn't circumvent security measures

### **Data Protection**
- **🔐 Secure Processing**: Encrypted credential handling
- **🗑️ Auto-Cleanup**: Temporary data removal
- **👤 Privacy Respect**: No unauthorized data collection
- **📖 Transparency**: Clear data usage policies

---

**Version**: 1.0  
**Last Updated**: July 2025  
**Status**: Active Development

---
