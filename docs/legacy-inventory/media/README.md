# Legacy Inventory — Media & Asset Storage Architecture

## 1. Storage Architecture Overview (`[FACT]`)

Based on source code analysis of `Amlakbashi.Host/Controllers/FileController.cs` and `Amlakbashi.Core/Entities/File.cs` from the recovered codebase:

* **Physical Upload Root:** Path relative to `IWebHostEnvironment.WebRootPath` (`Amlakbashi.Host/wwwroot/`).
* **Upload Directories:**
  - Property Residence Images: Mapped by `Entities.File.ResidenceImagesDirectory` (`wwwroot/Uploads/Residence/` or `wwwroot/Uploads/ResidenceImages/`), named using pattern `advertise_{accId}_{photoID}.jpg`.
  - Dynamically Generated Thumbnails Cache: Saved to `wwwroot/content/imgcache/img{FileID}_{w}_{h}.jpg` (or `.png`).
  - Fallback & Static Resources: Located under `wwwroot/resource/img/` (e.g. `/resource/img/img202_500_300.png`, `/resource/img/image-not-found-wide.png`).

---

## 2. Database File Entity Mapping (`[FACT]`)

Uploaded media records are tracked in the database `Files` table via the `Entities.File` C# class with key properties:
- `FileID` (Primary key, `bigint`)
- `FilePath` & `CorrectedFilePath` (Relative path string, e.g. `Uploads/...`)
- `Type` (`FileTypeEnum` e.g. `ResidenceImage`, `UserProfile`, `PostImage`)
- `MinifyStatus`, `MinifyQualityPercent`, `MinifyMaxWidth`
- `UserID`, `PostDate`, `LastModifyDate`

---

## 3. Storage Location & Recovery Mechanism (`[FACT]`)

* **Git Version Control Status:** User-uploaded property photos are excluded from Git version control (standard practice for multi-GB user upload media).
* **Recovery / Extraction Target:** To recover user-uploaded listing photos, the contents of the web server's `wwwroot/Uploads/` directory must be backed up from the production server host disk or cloud media volume.
