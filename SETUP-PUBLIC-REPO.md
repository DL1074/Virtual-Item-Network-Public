# Setting Up Your Public Distribution Repository

This guide will help you create a public GitHub repository for distributing VHN without exposing the source code.

## Step 1: Create New Public Repository

1. Go to GitHub and create a new repository
2. Name it: `Virtual-Hopper-Networks` or `VHN-Public`
3. Set visibility to **Public**
4. Do NOT initialize with README (we'll add our own)

## Step 2: Prepare Files for Public Repo

Copy these files from your private repo to the new public repo:

```
VHN-Public/
├── README.md              (use README-PUBLIC.md)
├── LICENSE                (use LICENSE-PUBLIC)
├── config.yml.example     (use config-example.yml)
└── .gitignore
```

### Files to Copy:

1. **README.md** - Copy from `README-PUBLIC.md`
2. **LICENSE** - Copy from `LICENSE-PUBLIC`
3. **config.yml.example** - Copy from `config-example.yml`

### Create .gitignore:

```gitignore
# Never commit source code
*.java
src/
pom.xml
target/

# Never commit built artifacts (use Releases instead)
*.jar

# IDE files
.idea/
.vscode/
*.iml
.classpath
.project
.settings/

# OS files
.DS_Store
Thumbs.db
```

## Step 3: Initial Commit

```bash
cd path/to/VHN-Public
git init
git add README.md LICENSE config.yml.example .gitignore
git commit -m "Initial commit - VHN public distribution"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/VHN-Public.git
git push -u origin main
```

## Step 4: Create First Release

1. Build your plugin: `mvn clean package`
2. Go to your public repo on GitHub
3. Click "Releases" → "Create a new release"
4. Tag version: `v1.0.0`
5. Release title: `VHN v1.0.0 - Initial Release`
6. Description:
   ```markdown
   ## VHN v1.0.0 - Initial Release
   
   High-performance hopper optimization for Minecraft Paper/Spigot servers.
   
   ### Features
   - 8-10x performance improvement over vanilla hoppers
   - Custom VHN hopper system with direct transfer
   - Idle network detection
   - Batch processing for large servers
   - 62-75% CPU reduction
   
   ### Installation
   1. Download `VHN-1.0.0.jar` below
   2. Place in `plugins/` folder
   3. Restart server
   4. Use `/vhn give <amount>` to get VHN hoppers
   
   ### Requirements
   - Paper or Spigot 1.20+
   - Java 17+
   
   See README for full documentation.
   ```
7. Upload `VHN-1.0.0.jar` from `target/` folder
8. Publish release

## Step 5: Update README Links

In your public README.md, update the download link:
```markdown
[Download Latest Release](https://github.com/YOUR-USERNAME/VHN-Public/releases/latest)
```

## Step 6: Repository Settings (Optional)

### Disable Features You Don't Need:
- Settings → Features → Uncheck "Wikis"
- Settings → Features → Uncheck "Projects"
- Settings → Features → Keep "Issues" (for bug reports)

### Add Repository Description:
```
High-performance hopper optimization plugin for Minecraft. 8-10x efficiency gains. Closed-source, JAR distribution only.
```

### Add Topics:
- `minecraft`
- `minecraft-plugin`
- `paper`
- `spigot`
- `hopper-optimization`
- `performance`

## Step 7: Maintaining Both Repositories

### Private Repo (Development):
- Keep all source code
- Continue development
- Commit regularly
- Keep technical README

### Public Repo (Distribution):
- Only documentation files
- No source code
- Upload JARs to Releases only
- User-friendly README

### Release Workflow:

1. Develop in private repo
2. Build: `mvn clean package`
3. Test thoroughly
4. Create release in public repo
5. Upload JAR file
6. Update changelog
7. Announce to users

## Step 8: Protecting Your Code

### What's Protected:
✅ Source code (never committed to public repo)
✅ Implementation details (removed from public README)
✅ Build configuration (pom.xml not included)
✅ Technical architecture (stripped from docs)

### What's Public:
✅ Compiled JAR (obfuscated by Java compilation)
✅ User documentation
✅ Configuration examples
✅ Commands and features

### Additional Protection (Optional):

If you want extra protection, use ProGuard to obfuscate the JAR:

```xml
<!-- Add to pom.xml in private repo -->
<plugin>
    <groupId>com.github.wvengen</groupId>
    <artifactId>proguard-maven-plugin</artifactId>
    <version>2.6.0</version>
    <executions>
        <execution>
            <phase>package</phase>
            <goals><goal>proguard</goal></goals>
        </execution>
    </executions>
</plugin>
```

This makes decompilation nearly impossible.

## Done!

You now have:
- ✅ Private repo for development
- ✅ Public repo for distribution
- ✅ Source code protection
- ✅ Professional documentation
- ✅ Proper licensing
- ✅ Release distribution system

Users can download and use VHN, but cannot see or modify the source code.
