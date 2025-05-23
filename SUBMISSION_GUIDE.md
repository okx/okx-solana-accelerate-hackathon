# OKX Solana Accelerate Hackathon - Submission Guide

This document provides comprehensive instructions for submitting your project to the OKX Solana Accelerate Hackathon.

We welcome projects that integrate OKX DEX API in innovative ways, including projects built by forking existing repositories such as well known DeFi protocols or AI Agents. The key is to demonstrate how you have utilized the OKX DEX API to enhance your project.

## Submission Methods

There are two ways to submit your project to the hackathon:

### Method 1: DoraHacks or HackQuest Platform Submission

If you registered through DoraHacks or HackQuest, you can submit directly through their platforms:

1. **DoraHacks**: Use the standard DoraHacks submission process on their platform
2. **HackQuest**: Follow the HackQuest submission workflow within their platform

**Important**: If you're using DoraHacks or HackQuest, you do NOT need to fork this repository or create a pull request. Simply use the submission process on the platform where you registered.

### Method 2: GitHub Repository Submission

If you prefer to submit through GitHub or didn't register through the platforms above, follow the detailed instructions below.

## Submission Process Overview (GitHub Method)
1. Fork this repository
2. Create your project using the provided templates
3. Submit a pull request with your complete project
4. Present your project during Demo Day

## Submission Requirements

### Required Files

For your submission, you need to include:

1. **submission.yaml** - Project metadata (required)
   - Basic project information
   - Team details
   - How you integrated OKX DEX API

2. **README.md** - Your project's documentation (format is flexible)
   - Explain what your project does
   - How to run your project
   - Any additional information you want to share

## How to Submit (GitHub Method)

1. Fork this repository
2. Create a new directory in the `submissions` folder with your team/project name
3. Add your submission.yaml file (see template in project-template/submission/)
4. Create a pull request to submit

## Detailed Instructions (GitHub Method)

### Step 1: Fork the Repository

1. Click the "Fork" button at the top right of this repository
2. This will create a copy of the repository in your GitHub account

### Step 2: Clone Your Fork

```bash
git clone https://github.com/okx/okx-solana-accelerate-hackathon.git
cd okx-solana-accelerate-hackathon
```

### Step 3: Create Your Project Directory

```bash
# Create a new directory for your project in the submissions folder
# Use a unique name without spaces (use hyphens instead)
mkdir -p submissions/your-project-name
```

### Step 4: Copy the Template Files

```bash
# Copy template files to your project directory
cp -r project-template/* submissions/your-project-name/
```

### Step 5: Add Your Project Files

1. Fill out the `README.md` with your project details
2. Update `submission.yaml` with your project metadata
3. Add any additional files needed (screenshots, code, etc.)

### Step 6: Commit and Push Your Changes

```bash
git add .
git commit -m "Add [Your Project Name] submission"
git push origin main
```

### Step 7: Create a Pull Request

1. Go to your fork on GitHub
2. Click "Contribute" then "Open Pull Request"
3. Fill out the PR template with your submission details
4. Submit your PR before the deadline (May 19, 2025, 11:59 PM UTC)

## For Projects with Existing Repositories

If you already have a complete project repository:

1. Fork this hackathon repository as usual
2. Create your submission directory: `submissions/your-project-name/`
3. Add the required files:
   - Copy your existing README.md
   - Create submission.yaml with a link to your main repo
   - Add demo video link and screenshots

4. In your submission.yaml, include:
   ```yaml
   repository_url: https://github.com/yourteam/existing-project
   main_repo: true  # Indicates code is in external repo

## Submission Requirements

All submissions must include (regardless of submission method):

### Required Files

1. **README.md** - Project documentation
   - Project name and description
   - Demo link or instructions to run
   - Features and functionality
   - OKX DEX API integration details
   - Technologies used
   - Setup and installation instructions

2. **submission.yaml** - Project metadata (GitHub submission only)
   - Project name, tagline, and track
   - Demo, repository, and video links
   - Technical details

3. **Demo Video** (Required)
   - Maximum 5 minutes in length
   - Demonstrate working functionality
   - Highlight OKX DEX API integration
   - Explain the problem and solution

4. **Screenshots/Images** (Recommended)
   - User interface screenshots
   - Architecture diagrams
   - Any relevant visuals

### Technical Requirements

1. **Working Demo**
   - Functional prototype or MVP
   - Integration with OKX DEX API
   - Deployable/runnable by judges

2. **Source Code**
   - Well-documented code
   - Setup instructions
   - Dependencies clearly listed

3. **OKX DEX API Integration**
   - Must use at least one feature of the OKX DEX API
   - Creative use of API features encouraged

## Judging Criteria

Submissions will be evaluated based on:

1. **Technical Implementation (30%)**
   - Code quality and complexity
   - Effective API integration
   - Innovation in technology stack

2. **User Experience (25%)**
   - Interface design
   - Usability and accessibility
   - Overall product polish

3. **Business Potential (20%)**
   - Market viability
   - Problem-solution fit
   - Scalability potential

4. **OKX Ecosystem Integration (15%)**
   - Leveraging OKX DEX features
   - Compatibility with OKX products
   - Integration potential

5. **Presentation Quality (10%)**
   - Demo clarity
   - Value proposition communication
   - Technical explanation

We look forward to seeing your innovative projects!
