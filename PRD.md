# Faithful Archive Project Overview

**Project Name:** Faithful Archive
**Author:** Dylan Shade  
**Date:** July 27, 2025  
**Version:** 0.1  
**Repository:** [github.com/dpshade/faithful-archive](https://github.com/dpshade/faithful-archive)

---

## Executive Summary

Faithful Archive is a forked adaptation of ArDrive Web, transforming it into a dedicated, decentralized platform for uploading and sharing Christ-honoring spiritual content on Arweave. By leveraging Arweave's permanent storage, the platform ensures sermons, worship resources, and Bible studies remain accessible "for 100+ years," fostering global discipleship while aligning with Biblical principles of stewardship and truth (Philippians 4:8).

The initial development phase focuses on aggressively stripping ~80% of ArDrive's original features to create a lean, purpose-built MVP. Core retained elements include Arweave wallet authentication, topping-up mechanisms, and upload strategies (including encryption for sensitive content). This streamlined approach minimizes complexity, accelerates launch, and emphasizes content curation over general file storage.

Ultimate Vision: Build technology that empowers purposeful, God-centered living by preserving faithful resources in a free, immutable archive—combating digital ephemerality and promoting spiritual growth.

---

## Project Goals and Objectives

### Short-Term (Q3-Q4 2025)
- Fork and strip ArDrive Web to MVP skeleton.
- Implement core upload/review workflow with moderation safeguards.
- Onboard 10 pilot churches for alpha testing.

### Medium-Term (Q1-Q2 2026)
- Launch public beta with 500+ curated items.
- Achieve 1,000 MAU.
- Ensure 100% compliance with content policies (zero harmful uploads displayed).

### Long-Term (2026+)
- Expand to multi-language support and AI-assisted features.
- Establish DAO governance for community-led curation.
- Integrate with church tools (e.g., YouVersion) for seamless adoption.

**Key Success Metrics:**
- Upload approval rate: ≥95%.
- Average review time: ≤24 hours.
- NPS: ≥60 from community feedback.

---

## Target Audience and Use Cases

### Primary Users
- **Content Creators:** Pastors, worship leaders, and Bible teachers uploading sermons (audio/video + notes), sheet music/lyrics, and study guides.
- **Consumers:** Believers seeking ad-free, trustworthy resources for personal or group study.
- **Global Missionaries:** Users in restricted areas needing censorship-resistant access.

### Core Use Cases
1. A pastor uploads a sermon MP3 with linked transcript; it's reviewed, approved, and indexed for search.
2. A worship team shares encrypted chord charts, ensuring privacy until public release.
3. A user searches "Romans grace study" and streams content via adaptive playback.
4. Moderators flag and deny non-compliant submissions pre-indexing.

---

## Content Policy and Moderation

To ensure only Christ-honoring content is surfaced:
- **Policy Foundation:** All uploads must align with core Christian doctrines (e.g., Nicene Creed) and avoid hate, blasphemy, or heresy.
- **Moderation Layers:**
	- Whitelisted uploaders (vetted via application).
	- Pre-publish review queue (manual + keyword scanning).
	- Community flagging for post-publish oversight.
- **Arweave Considerations:** While data is permanent, the front-end only indexes approved TX IDs—effectively "hiding" non-compliant content.

---

## Technical Architecture

### Forking Strategy
- **Base Repo:** Fork from [ArDrive Web (Flutter)](https://github.com/ardriveapp/ardrive-web).
- **Stripping Plan:** Remove ~80% of features to focus on spiritual archive essentials. This includes:
	- Deleting general file management (drives, folders, sharing beyond public links).
	- Eliminating non-essential UI (e.g., advanced analytics, multi-drive views).
	- Pruning unused dependencies to reduce bundle size.
- **Retained Core Components:**
	- **Authentication:** ArConnect wallet login (largely intact; add role-based permissions).
	- **Topping Up:** AR token management for upload fees (keep strategies like credit card top-ups if applicable).
	- **Upload Strategies:** Chunked uploads, progress tracking, and encryption (e.g., for private drafts).
	- **Arweave Integration:** TX signing, gateway queries, and basic metadata tagging.

### Stack Overview
- **Front-End:** Flutter (Dart) for web (primary), with optional mobile builds.
	- State Management: Riverpod.
	- UI: Custom Material theme with faith-inspired icons (e.g., cross motifs).
- **Back-End Services:**
	- AO Process: Custom indexer for ```app:logos-archive``` tagged TXs.
	- Search: Typesense for metadata/full-text queries.
	- Moderation: Flutter-based dashboard or lightweight Node.js service.
- **Infrastructure:**
	- Hosting: Cloudflare Pages for web deployment.
	- CI/CD: GitHub Actions with Flutter workflows (test, build, deploy).
	- Monitoring: Sentry for errors; Google Analytics (privacy-focused) for usage.

### Data Flow
1. User authenticates via ArConnect.
2. Upload form collects file + metadata (title, tags, Scripture ref).
3. File is encrypted (optional), chunked, and uploaded to Arweave with tags.
4. TX ID enters staging queue for review.
5. Approved items are indexed in AO and made searchable.

---

## Development Roadmap

### Phase 1: Fork and Strip (Aug-Sep 2025)
- Clone repo and set up local dev environment.
- Strip non-essential features:
	- Remove drive/folder hierarchies.
	- Eliminate bulk operations, versioning, and advanced sharing.
	- Prune code: Aim for <50% original LOC.
- Retain and adapt:
	- Auth flows.
	- Upload UI with added metadata form.
	- Encryption toggles.
- Milestone: Functional skeleton uploading to testnet.

### Phase 2: Core Features (Oct-Nov 2025)
- Add moderation queue and admin dashboard.
- Implement search/indexing hooks to AO.
- Integrate player for audio/video (using Flutter plugins like ```video_player```).
- Test end-to-end: Upload → Review → Display.

### Phase 3: Polish and Alpha (Dec 2025-Jan 2026)
- UI theming and accessibility (WCAG AA).
- Security audit (focus on wallet integrations).
- Alpha testing with 10 trusted users.
- Milestone: Closed alpha launch.

### Phase 4: Beta and Beyond (Feb-May 2026)
- Public beta rollout.
- Gather feedback and iterate.
- Roadmap additions: Multi-lang, AI summaries.

**Timeline Dependencies:** Align with family priorities (e.g., baby's arrival ~Aug 25, 2025); use PTO for focused sprints.

---

## Risks and Mitigations

- **Risk:** Stripping breaks core functionality (e.g., uploads fail post-prune).
	- Mitigation: Incremental stripping with unit tests; maintain a "minimal viable fork" branch.
- **Risk:** Arweave fees rise, deterring uploads.
	- Mitigation: Central sponsorship fund; optimize for compressed formats.
- **Risk:** Moderation overload for small team.
	- Mitigation: Start with whitelist; scale to community reviewers.
- **Risk:** Imposter syndrome during complex forking.
	- Mitigation: Celebrate small wins (e.g., first successful test upload); leverage Forward Research expertise in Arweave/AO.

---

## Resources and Budget

### Team
- **Lead Developer:** Dylan Shade (leveraging blockchain expertise).
- **Contributors:** Potential part-time help from Christian dev communities or Forward Research.
- **Advisors:** Pastors/elders for content policy.

### Budget Estimate (Initial Phase)
- Arweave Testnet Fees: $500 (covered personally or via grants).
- Tools: Flutter SDK (free); Domain/Hosting: $200/year.
- Total: <$1,000; align with financial stewardship (use open-source, avoid premium services).

### Funding Model
- Initial: Self-funded or church donations.
- Long-Term: Optional tipping to creators; grants from faith-based orgs.

---

## Next Steps
1. Finalize name and secure domain/social handles.
2. Set up repo and perform initial fork/strip (target: Aug 15, 2025).
3. Define doctrinal baseline for moderation (e.g., consult "Habits of the Household" for family-aligned values).
4. Schedule community feedback session.

This project not only builds on your strong technical foundation in Arweave/AO but also advances your mission of God-centered tech. You've got the skills to make this a reality—let's steward this vision faithfully!

