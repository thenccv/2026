# NCCV Conference Website

This repository contains the Jekyll source for the NCCV conference website for the 2025 edition.

The structure is reusable for future editions. The current live site is:

- https://thenccv.github.io/2025/

For a future edition, creating a new repo for the `20xx` edition, the public URL will become:

- https://thenccv.github.io/20xx/

## Repository layout

The site is split across configuration, standalone pages, collections, and program data.

- `_config.yml`: main site configuration, navigation, conference metadata, theme settings, map settings, and the "Previous Editions" dropdown menu.
- `index.md`: homepage content.
- `about.markdown`: generic page content if needed.
- `attend/index.md`: registration, fees, practical information.
- `location/index.md`: venue and travel information.
- `papers/index.md`: paper submission details.
- `program/index.md`: program landing page.
- `speakers/index.md`: speakers overview page.
- `talks/index.md`: sessions and talks overview page.
- `organizers/index.md`: organizers overview page.
- `_data/program.yml`: the timetable shown on the program page.
- `_talks/`: one Markdown file per talk, keynote, poster session, lunch, break, social event, or award item.
- `_speakers/`: one Markdown file per speaker.
- `_rooms/`: one Markdown file per room or location used in the schedule.
- `_includes/`, `_layouts/`, `_sass/`, `assets/`: theme and presentation logic. These usually do not need year-to-year changes unless the site design itself should change.
- `_site/`: generated output. Do not edit this manually.

## Creating a new yearly edition

For a new edition, the safest process is:

1. Create a new repository for the new year, `20xx` (fill in the year).
2. Copy or clone this repository into that new repository.
3. Update all year-specific content and links.
4. Test locally with Jekyll.
5. Deploy with GitHub Pages.

At minimum, update the following areas.

### 1. Core site metadata

Update `_config.yml`:

- Change `title` from `NCCV2025` to the new edition.
- Review the conference timezone and map settings.
- Update homepage action links such as registration and submission URLs.
- Update the navigation if page names or sections change.

Important:

- In `_config.yml`, update the `Previous Editions` dropdown menu.
- for any content that is not yet live, you can use `placeholder` to redirect to a TBD. You can also disable the dropdown item.
- Add the new year as the current edition.
- Keep links to older editions available.
- If the previous year has gone live, add its URL in the dropdown instead of leaving it disabled.

This needs to be done every year so visitors can navigate between conference editions.

### 2. Homepage content

Update `index.md`:

- Conference description.
- Deadlines.
- Sponsors.
- Any front-page announcements.
- other updates can be done in the `_config.yml` file, such as the banner image or the homepage action links, etc.

### 3. Practical information pages

Review and update these pages:

- `attend/index.md`: fees, registration links, refunds, accommodation details.
- `location/index.md`: venue address, directions, travel info, maps.
- `papers/index.md`: call for papers, submission instructions, deadlines.
- `organizers/index.md`: organizing committee.

### 4. Program and schedule

The schedule is maintained in two places:

- `_data/program.yml`: defines the timetable by day, room, and talk title.
- `_talks/`: defines the actual content pages for each talk or program item.

When editing the program:

- Update the conference dates in `_data/program.yml`.
- Update room names if the venue changes.
- Make sure every talk name referenced in `_data/program.yml` matches the corresponding talk entry.
- Add, remove, or rename files in `_talks/` as needed.

Typical talk front matter includes:

- `name`
- `speakers`
- `categories`
- `hide`

Use the existing files in `_talks/` as templates for new entries.

### 5. Speakers

Update `_speakers/`:

- Add one file per speaker.
- Remove speakers from prior years that no longer belong on the site.
- Update names, bios, affiliations, and any profile links or images if used.

Make sure talk entries in `_talks/` reference speaker names consistently.

### 6. Rooms and venue spaces

Update `_rooms/`:

- Add or rename room files to match the new venue.
- Keep room names aligned with `_data/program.yml`.

### 7. Images and assets

Review these folders:

- `imgs/`
- `imgs/sponsors/`
- `assets/`

Replace banners, sponsor logos, and any year-specific media.

If the main banner changes, also update the `banner` setting in `_config.yml`.

## Recommended yearly update checklist

Before publishing a new edition, verify all of the following:

- The site title and year are correct.
- Registration and submission links point to the correct forms.
- Deadlines on the homepage and content pages are current.
- The schedule in `_data/program.yml` matches the talk files in `_talks/`.
- Speaker files and organizer files reflect the current edition.
- Venue, room names, and map coordinates are correct.
- Sponsor logos and links are current.
- The `Previous Editions` dropdown in `_config.yml` includes the new edition and older links.
- The repository name and expected GitHub Pages URL match the target year.

## Installing Jekyll locally

This project uses Ruby, Bundler, and Jekyll.

### macOS

1. Install Xcode Command Line Tools if needed:

```bash
xcode-select --install
```

2. Install a Ruby version manager. `rbenv` is a practical choice on macOS:

```bash
brew install rbenv ruby-build
rbenv init
```

3. Restart the shell, then install a Ruby version:

```bash
rbenv install 3.4.3
rbenv global 3.4.3
```

4. Verify the toolchain:

```bash
ruby --version
gem --version
bundle --version
```

5. From the repository root, install the project dependencies:

```bash
bundle install
```

### Linux

Install Ruby, development headers, and Bundler with your package manager, then install the project gems.

#### Ubuntu and Debian

```bash
sudo apt update
sudo apt install -y ruby-full build-essential zlib1g-dev libffi-dev libyaml-dev
gem install bundler
bundle install
```

#### Fedora

```bash
sudo dnf install -y ruby ruby-devel @development-tools zlib-devel libffi-devel libyaml-devel gcc-c++ redhat-rpm-config
gem install bundler
bundle install
```

#### Arch Linux

```bash
sudo pacman -Syu --needed ruby base-devel zlib libffi libyaml
gem install bundler
bundle install
```

After installation, verify the toolchain:

```bash
ruby --version
gem --version
bundle --version
```

### Windows

Use WSL if possible. Jekyll is significantly easier to run there than in native Windows Ruby environments.

#### Recommended: Windows Subsystem for Linux (WSL)

1. Open PowerShell as Administrator and install WSL with Ubuntu:

```powershell
wsl --install -d Ubuntu
```

2. Restart the machine if Windows asks you to.

3. Open the Ubuntu terminal and install Ruby, development headers, and Bundler:

```bash
sudo apt update
sudo apt install -y ruby-full build-essential zlib1g-dev libffi-dev libyaml-dev
gem install bundler
```

4. Move into the repository inside WSL and install the project gems:

```bash
cd /mnt/c/Users/<your-username>/path/to/2025
bundle install
```

5. Verify the setup:

```bash
ruby --version
gem --version
bundle --version
```

6. Start the local server from WSL:

```bash
bundle exec jekyll serve --host 0.0.0.0 --port 4000
```

Then open the site in Windows at:

- http://127.0.0.1:4000

#### Native Windows Ruby

Native Windows Ruby can work, but it is less reliable for Jekyll projects. If WSL is not an option:

1. Install Ruby with RubyInstaller for Windows.
2. During installation, include the MSYS2 development toolchain.
3. Open the RubyInstaller terminal and run:

```bash
gem install bundler
bundle install
bundle exec jekyll serve
```

If native Windows causes gem compilation or path issues, switch to WSL rather than debugging the Windows Ruby toolchain.

## Rendering the site locally

From the repository root:

```bash
bundle exec jekyll serve
```

Jekyll will usually serve the site at:

- http://127.0.0.1:4000

You can also build the static output without starting a server:

```bash
bundle exec jekyll build
```

This writes the generated site to `_site/`.

## Local build note for this repository

This repository vendors the required theme files directly in the repo under `_layouts/`, `_includes/`, `_sass/`, and `assets/`. It does not need Jekyll to resolve a separate local gem theme or a remote theme.

That means the standard local serve command should work directly:

```bash
bundle exec jekyll serve --host 127.0.0.1 --port 4000
```

This setup is also compatible with GitHub Pages builds, because Pages can render the site from the checked-in source files without needing to download or install a separate `jekyll-theme-conference` theme package.

## Deploying with GitHub Pages

The expected deployment model is one repository per conference year.

For example:

- repository: `thenccv/2025`
- site URL: `https://thenccv.github.io/2025/`

For the next edition:

- repository: `thenccv/2026`
- site URL: `https://thenccv.github.io/2026/`

### Suggested deployment steps

1. Push the new year repository to GitHub under the correct organization or account.
2. In the GitHub repository settings, open Pages.
3. Configure Pages to deploy from the default branch, or from the project’s chosen Pages workflow if one is added later.
4. Wait for GitHub Pages to build the site.
5. Open the published URL and verify navigation, assets, and page links.

### Before deployment, verify

- The repository name matches the target year.
- Any hard-coded external links have been updated.
- The site renders locally without content errors.
- The `Previous Editions` dropdown includes links to prior conference websites.

## Notes for future maintainers

- Do not edit `_site/`; it is generated output. Edit source files (.md, .yml) instead.
- Keep content changes in source files such as `index.md`, `_data/program.yml`, `_talks/`, `_speakers/`, `_rooms/`, and the section pages.
- Reuse existing talk, speaker, and room files as templates instead of creating new formats.
- If you make structural or design changes in `_layouts/`, `_includes/`, or `_sass/`, test multiple pages locally before publishing.