# Tyler Schrock Portfolio

Static portfolio site for Tyler Schrock, focused on platform engineering, site reliability, DevOps, Linux systems, automation, monitoring, security tooling, and infrastructure operations.

The site is intentionally simple: HTML, CSS, a small amount of JavaScript, local images, and an Nginx-based Docker image for serving the content.

## Site Contents

- `index.html` - Homepage, featured projects, resume link, and contact form.
- `about_me.html` - Professional background, education, and career summary.
- `site_architecture.html` - Overview of how the site is built and hosted, including Kubernetes/home lab deployment details.
- `projects/` - Individual project case studies.
- `css/responsive-attributes.css` - Layout, responsive behavior, and visual styling.
- `images/` - Architecture diagrams and supporting images.
- `files/` - Static downloadable files, including the resume PDF.
- `Dockerfile` - Nginx container image definition for serving the static site.
- `.dockerignore` - Keeps Git metadata, local temp files, logs, and OS/editor artifacts out of Docker build contexts.

## Featured Project Areas

The portfolio highlights work across several infrastructure and operations domains:

- CrowdStrike Falcon deployment automation across a large Linux server environment.
- OpenVPN Access Server design for segmented vendor access.
- JFrog Artifactory and Xray for artifact management and software supply chain visibility.
- Zabbix monitoring for Linux, Windows, and SNMP-enabled infrastructure.
- Canonical Landscape for controlled Linux patch management.
- IBM Change Data Capture for enterprise data replication workflows.

The project pages are written as generalized case studies. Proprietary code, credentials, internal hostnames, and sensitive infrastructure details are intentionally excluded.

## Running Locally

Because this is a static site, it can be opened directly in a browser:

```bash
open index.html
```

Or served with a lightweight local web server:

```bash
python3 -m http.server 8080
```

Then visit:

```text
http://localhost:8080
```

## Running With Docker

Build the image:

```bash
docker build -t tschrock52-html-site .
```

Run the container:

```bash
docker run --rm -p 8080:80 tschrock52-html-site
```

Then visit:

```text
http://localhost:8080
```

## Deployment Notes

The live deployment approach is documented in `site_architecture.html`.

At a high level, the site is served as a static Nginx container and deployed into a Kubernetes environment. Public traffic flows through DNS, pfSense/HAProxy, ingress-nginx, Kubernetes Services, and site pods. MetalLB is used to provide LoadBalancer-style access inside the home lab environment.

The architecture page also documents the lightweight local build/deploy workflow used for this site, including Docker image creation, Docker Hub publishing, and Kubernetes rollout commands.

## External Dependencies

The site uses a few CDN-hosted frontend assets:

- Font Awesome for brand/navigation icons.
- Google Fonts for typography.
- Lucide icons for the resume link icon.
- Highlight.js on selected project pages for code formatting.

If offline or fully self-contained hosting is required, these assets should be vendored locally.

## Maintenance Notes

- Keep project pages generalized and free of proprietary implementation details.
- Validate links after changing page paths or moving images.
- Keep resume content in `files/` current.
- When adding a new project, update the project navigation on each page or move the shared layout to a template/static-site generator.
- Keep `.dockerignore` current if local tooling, generated files, or private configuration files are added later.

## Future Improvements

- Add shared page templates or migrate to a small static site generator to reduce duplicated navigation, sidebar, and JavaScript.
- Add accessible accordion state handling with `aria-expanded` and `aria-controls`.
- Convert image modal close controls to semantic buttons.
- Add basic link checking and HTML validation to the maintenance workflow.
- Expand repository documentation if Kubernetes manifests or deployment scripts are added directly to this repo.
