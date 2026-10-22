<div align="center">

<img src="https://imgbs.com/uploads/copyright-mileina-0b70b07f.png" alt="Copyright © MILEINA">

# MILEINA CHATBOT

Multi-device WhatsApp bot built on Node.js and the Baileys library. It provides hundreds of commands through a modular plugin system, covering AI, sticker creation, image and media makers, group management, and utilities. Developed by Hai Ell Engineer.

![Build Status](https://img.shields.io/badge/build-passing-brightgreen)
![Version](https://img.shields.io/badge/version-1.185.7-blue)
![License](https://img.shields.io/badge/license-MIT-yellow)
![Node](https://img.shields.io/badge/node-%3E%3D24-6DA55F)
![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen)

[Demo](#) · [Documentation](#) · [Report Bug](https://github.com/username/nama-repo/issues) · [Request Feature](https://github.com/username/nama-repo/issues)

</div>

---

## 📋 Table of Contents

- [About](#-about)
- [Features](#-features)
- [Requirements](#-requirements)
- [Installation](#-installation)
- [Usage](#-usage)
- [Project Structure](#-project-structure)
- [Architecture](#-architecture)
- [Configuration](#-configuration)
- [Creating a Plugin](#-creating-a-plugin)
- [Tech Stack](#-tech-stack)
- [Roadmap](#-roadmap)
- [Contributing](#-contributing)
- [FAQ](#-faq)
- [License](#-license)
- [Contact](#-contact)
- [Acknowledgements](#-acknowledgements)

---

## 📖 About

MILEINA is a WhatsApp bot written in Node.js with ESM modules, running on the Baileys library with multi-device support. Every command is designed to be concise: type it and get an immediate result, with no complicated input formatting.

The codebase follows one consistent pattern across all plugins, so anyone exploring the project can understand the workflow quickly and keep developing it.

> Developed and maintained by **Hai Ell Engineer**, following the principle: *"From the original developers, for the next developers."*
>
> **Tip:** Before adding or changing anything, read the existing workflows and follow the established patterns instead of introducing new ones.

## ✨ Features

- **AI**: chat and AI-powered commands (97 plugins).
- **Maker**: image and media generators (79 plugins).
- **Sticker**: create stickers from images, videos, and GIFs (32 plugins).
- **Group**: group management tools with admin and bot-admin checks (27 plugins).
- **Developer**: maintenance and debugging commands for the developer role (21 plugins).
- **Random**: random image fetchers (14 plugins).
- **Tools, Upload, Main**: utilities, file uploads, and the main menu.
- **Hot reload**: plugins are reloaded when their files change, without restarting the bot.
- **Access control**: per-command flags for group, private chat, admin, bot admin, developer, registration, and usage limits.
- **Multiple providers**: external API providers and local random-image sources, with shared error handling.

## 🧰 Requirements

- **Node.js 24 or later** (set in `engines`).
- **ffmpeg**: used for voice notes and media conversion. The `@ffmpeg-installer/ffmpeg` package is included, but a system install is recommended for stability.
- **Build tools** for native modules such as `canvas` and `sharp`, if prebuilt binaries are not available for your platform.
- A WhatsApp account to use as the bot number.

## ⚙️ Installation

Clone the repository:

```bash
git clone https://github.com/npmEll001/mileinaProjects.git
cd mileinaProjects
```

Install dependencies:

```bash
npm install
```

Start the bot:

```bash
npm start
```

For development with auto-restart:

```bash
npm run dev
```

On first run, the bot prints a pairing code (or a QR code, depending on `Bot.pairing.useQR`). Enter the code in WhatsApp under **Linked Devices**. The session is saved to the session folder, so you do not need to log in again while it stays valid.

### Hosting Panels (Pterodactyl)

1. Upload all project files, or upload a `.zip` and extract it.
2. Delete `node_modules`, the session folder, and `package-lock.json` if they exist.
3. Select **Node.js 24** in the startup settings.
4. Edit the configuration files (see [Configuration](#-configuration)).
5. Run `npm install`, then `npm start`.

### Termux

```bash
pkg update && pkg upgrade -y
pkg install nodejs-lts git -y
termux-setup-storage
cd ~
cp -r "/storage/emulated/0/Download/YOUR_FOLDER" .
cd "YOUR_FOLDER"
rm -rf node_modules package-lock.json
node -v && npm -v
npm install
npm start
```

## 🚀 Usage

Commands start with the prefix set in `globalBot.js` (default `.`).

```
.menu            → main menu
.menu <key>      → menu for one category
.menu all        → all commands
```

Examples:

```
.getlinkgc       → get the group invite link (group, admin, bot admin)
```

## 🗂️ Project Structure

<details>
<summary>Klik untuk melihat struktur folder lengkap</summary>

```
mileinaProjects/
├── library/
│   ├── databases/
│   │   ├── bots/
│   │   │   ├── botPath.js
│   │   │   ├── defaultBot.js
│   │   │   ├── deleteBot.js
│   │   │   ├── getAllBots.js
│   │   │   ├── getBot.js
│   │   │   ├── hasBot.js
│   │   │   ├── incrementBot.js
│   │   │   ├── resetBot.js
│   │   │   ├── setBot.js
│   │   │   ├── setBotCustom.js
│   │   │   └── updateBot.js
│   │   ├── groups/
│   │   │   ├── createGroup.js
│   │   │   ├── defaultGroup.js
│   │   │   ├── deleteGroup.js
│   │   │   ├── getAllGroups.js
│   │   │   ├── getGroup.js
│   │   │   ├── groupPath.js
│   │   │   ├── hasGroup.js
│   │   │   ├── incrementGroup.js
│   │   │   ├── resetGroup.js
│   │   │   ├── setGroup.js
│   │   │   ├── setGroupCustom.js
│   │   │   └── updateGroup.js
│   │   ├── sharedDatabases/
│   │   │   ├── ensureDirs.js
│   │   │   ├── getDirs.js
│   │   │   ├── getNested.js
│   │   │   ├── isFlatObject.js
│   │   │   ├── isPrimitive.js
│   │   │   ├── prettyStringify.js
│   │   │   ├── readJSON.js
│   │   │   ├── registryDatabases.js
│   │   │   ├── setNested.js
│   │   │   ├── timeDatabase.js
│   │   │   └── writeJSON.js
│   │   ├── sharedDataDefaults/
│   │   │   ├── botModes/
│   │   │   │   ├── botBehaviors/
│   │   │   │   │   ├── modeDev.js
│   │   │   │   │   └── noPm.js
│   │   │   │   └── importBotModes.js
│   │   │   ├── groupModes/
│   │   │   │   ├── groupBehaviors/
│   │   │   │   │   ├── autoBye.js
│   │   │   │   │   ├── autoDetect.js
│   │   │   │   │   ├── autoShalat.js
│   │   │   │   │   ├── autoWelcome.js
│   │   │   │   │   ├── modeAdmin.js
│   │   │   │   │   ├── noAudio.js
│   │   │   │   │   ├── noContact.js
│   │   │   │   │   ├── noDelete.js
│   │   │   │   │   ├── noDocument.js
│   │   │   │   │   ├── noEvent.js
│   │   │   │   │   ├── noForward.js
│   │   │   │   │   ├── noImage.js
│   │   │   │   │   ├── noLinkAll.js
│   │   │   │   │   ├── noLinkWa.js
│   │   │   │   │   ├── noLocation.js
│   │   │   │   │   ├── noPolling.js
│   │   │   │   │   ├── noSpam.js
│   │   │   │   │   ├── noSticker.js
│   │   │   │   │   ├── noTagStatus.js
│   │   │   │   │   ├── noVideo.js
│   │   │   │   │   └── noVideoNote.js
│   │   │   │   └── importGroupModes.js
│   │   │   └── importSharedDataDefaults.js
│   │   ├── users/
│   │   │   ├── defaultUser.js
│   │   │   ├── deleteUser.js
│   │   │   ├── getAllUsers.js
│   │   │   ├── getUser.js
│   │   │   ├── hasUser.js
│   │   │   ├── incrementUser.js
│   │   │   ├── resetUser.js
│   │   │   ├── setUser.js
│   │   │   ├── setUserCustom.js
│   │   │   ├── updateUser.js
│   │   │   └── userPath.js
│   │   ├── clearDatabase.js
│   │   └── importDatabases.js
│   ├── errors/
│   │   └── ApiError.js
│   ├── modules/
│   │   ├── adjustables/
│   │   │   ├── configs/
│   │   │   │   ├── globalApi.js
│   │   │   │   ├── globalBadge.js
│   │   │   │   ├── globalBot.js
│   │   │   │   ├── globalDev.js
│   │   │   │   ├── globalEventMsg.js
│   │   │   │   ├── globalExclude.js
│   │   │   │   ├── globalFallback.js
│   │   │   │   ├── globalGroupText.js
│   │   │   │   ├── globalInterval.js
│   │   │   │   ├── globalMapEmoji.js
│   │   │   │   ├── globalMedia.js
│   │   │   │   ├── globalMessage.js
│   │   │   │   ├── globalPackname.js
│   │   │   │   ├── globalPayments.js
│   │   │   │   ├── globalSchedule.js
│   │   │   │   ├── globalScrape.js
│   │   │   │   ├── globalShalat.js
│   │   │   │   ├── globalSosial.js
│   │   │   │   ├── globalTime.js
│   │   │   │   ├── globalTTL.js
│   │   │   │   ├── globalUser.js
│   │   │   │   └── globalWebsite.js
│   │   │   └── importAdjustables.js
│   │   ├── caches/
│   │   │   ├── groupMetadataCaches/
│   │   │   │   ├── getCachedGroupMetadata.js
│   │   │   │   └── invalidateGroupMetadataCache.js
│   │   │   ├── menuSectionsCaches/
│   │   │   │   ├── getCachedMenuSections.js
│   │   │   │   └── invalidateMenuSectionsCache.js
│   │   │   ├── noDeleteCaches/
│   │   │   │   ├── cacheMessageForDelete.js
│   │   │   │   ├── clearDeletedMessageCache.js
│   │   │   │   └── getDeletedMessageCache.js
│   │   │   ├── profilePictureCaches/
│   │   │   │   ├── getCachedProfilePicture.js
│   │   │   │   ├── invalidateAllProfilePictureCache.js
│   │   │   │   └── invalidateProfilePictureCache.js
│   │   │   ├── sharedCaches/
│   │   │   │   └── registryCaches.js
│   │   │   ├── spamCaches/
│   │   │   │   ├── addSpamCache.js
│   │   │   │   └── resetSpamCache.js
│   │   │   ├── thumbnailCaches/
│   │   │   │   ├── getCachedThumbnail.js
│   │   │   │   ├── invalidateAllThumbnailCache.js
│   │   │   │   └── invalidateThumbnailCache.js
│   │   │   └── importCaches.js
│   │   ├── events/
│   │   │   ├── groupEvents/
│   │   │   │   ├── localGroupSettings/
│   │   │   │   │   ├── localGroupSettingText.js
│   │   │   │   │   ├── localMemberText.js
│   │   │   │   │   ├── mediaTypeMap.js
│   │   │   │   │   ├── mergeGroupText.js
│   │   │   │   │   └── modeMap.js
│   │   │   │   ├── checkSpam.js
│   │   │   │   ├── groupModeFilter.js
│   │   │   │   ├── groupUpdate.js
│   │   │   │   ├── handleAfkDetection.js
│   │   │   │   ├── handleContactUpdate.js
│   │   │   │   ├── handleGroupJoinRequest.js
│   │   │   │   ├── handleNoDelete.js
│   │   │   │   └── participantUpdate.js
│   │   │   ├── participantEvents/
│   │   │   │   ├── handleGroupParticipantsUpdate.js
│   │   │   │   └── handleGroupUpdate.js
│   │   │   └── importEvents.js
│   │   ├── groupParticipants/
│   │   │   ├── sharedGroupParticipants/
│   │   │   │   ├── decodeJid.js
│   │   │   │   ├── getGroupParticipantData.js
│   │   │   │   ├── isBotJid.js
│   │   │   │   ├── isSameUser.js
│   │   │   │   ├── mentionJid.js
│   │   │   │   ├── messageTargets.js
│   │   │   │   ├── normalizeNumber.js
│   │   │   │   └── resolveDisplayJid.js
│   │   │   └── importGroupParticipants.js
│   │   ├── loaders/
│   │   │   ├── hotReload.js
│   │   │   └── runPlugin.js
│   │   ├── rootProtokols/
│   │   │   ├── enhancedsProtokols/
│   │   │   │   ├── enchanteds/
│   │   │   │   │   ├── deleteByKey.js
│   │   │   │   │   ├── download.js
│   │   │   │   │   ├── eventMsg.js
│   │   │   │   │   ├── profilePicture.js
│   │   │   │   │   ├── react.js
│   │   │   │   │   ├── reply.js
│   │   │   │   │   ├── replyAIRich.js
│   │   │   │   │   ├── replyCarousel.js
│   │   │   │   │   ├── replyCodeBlock.js
│   │   │   │   │   ├── replyImage.js
│   │   │   │   │   ├── replyProfileDoc.js
│   │   │   │   │   ├── replySticker.js
│   │   │   │   │   └── replyVideo.js
│   │   │   │   └── importEnchancedProtokols.js
│   │   │   ├── messageProtokols/
│   │   │   │   ├── rootMessages/
│   │   │   │   │   ├── customMessages/
│   │   │   │   │   │   ├── allLinkMessage.js
│   │   │   │   │   │   ├── forwardedMessage.js
│   │   │   │   │   │   ├── groupStatusMentionMessage.js
│   │   │   │   │   │   └── waLinkMessage.js
│   │   │   │   │   ├── nativeMessages/
│   │   │   │   │   │   ├── audioMessage.js
│   │   │   │   │   │   ├── contactMessage.js
│   │   │   │   │   │   ├── contactsArrayMessage.js
│   │   │   │   │   │   ├── conversation.js
│   │   │   │   │   │   ├── documentMessage.js
│   │   │   │   │   │   ├── eventMessage.js
│   │   │   │   │   │   ├── extendedTextMessage.js
│   │   │   │   │   │   ├── imageMessage.js
│   │   │   │   │   │   ├── liveLocationMessage.js
│   │   │   │   │   │   ├── locationMessage.js
│   │   │   │   │   │   ├── pollCreationMessage.js
│   │   │   │   │   │   ├── pollCreationMessageV3.js
│   │   │   │   │   │   ├── ptvMessage.js
│   │   │   │   │   │   ├── stickerMessage.js
│   │   │   │   │   │   └── videoMessage.js
│   │   │   │   │   └── importRootMessages.js
│   │   │   │   └── importMessageProtokols.js
│   │   │   ├── sharedRootProtokols/
│   │   │   │   ├── airichProof.js
│   │   │   │   ├── buildQuoted.js
│   │   │   │   ├── buildVcardQuoted.js
│   │   │   │   ├── constants.js
│   │   │   │   ├── getBody.js
│   │   │   │   ├── getMentionedJid.js
│   │   │   │   ├── sendRich.js
│   │   │   │   └── thumbnail.js
│   │   │   └── serializeMessage.js
│   │   ├── schedulers/
│   │   │   ├── checkerSchedulers/
│   │   │   │   ├── checkAutoShalat.js
│   │   │   │   ├── checkDailyLimitReset.js
│   │   │   │   ├── checkExpiredAfk.js
│   │   │   │   ├── checkExpiredGroupAccess.js
│   │   │   │   └── checkRemainingGroupAccess.js
│   │   │   ├── sharedSchedulers/
│   │   │   │   ├── registrySchedulers.js
│   │   │   │   ├── schedulerKit.js
│   │   │   │   └── taskRunner.js
│   │   │   └── importSchedulers.js
│   │   ├── validations/
│   │   │   ├── validators/
│   │   │   │   ├── alphanumeric.js
│   │   │   │   ├── aspectRatio.js
│   │   │   │   ├── constants.js
│   │   │   │   ├── maxFileSize.js
│   │   │   │   ├── maxLength.js
│   │   │   │   ├── minWordCount.js
│   │   │   │   ├── noEmoji.js
│   │   │   │   ├── notEmpty.js
│   │   │   │   ├── number.js
│   │   │   │   ├── quotedMedia.js
│   │   │   │   ├── regexMatch.js
│   │   │   │   └── videoDuration.js
│   │   │   └── importValidations.js
│   │   ├── denyAccess.js
│   │   ├── importModules.js
│   │   └── profile.js
│   ├── providers/
│   │   ├── APIs/
│   │   │   ├── providerAPIs/
│   │   │   │   ├── azbry.js
│   │   │   │   ├── bintang.js
│   │   │   │   ├── cmnty.js
│   │   │   │   ├── deline.js
│   │   │   │   ├── evelyne.js
│   │   │   │   ├── faa.js
│   │   │   │   ├── ikyyxd.js
│   │   │   │   ├── neoxr.js
│   │   │   │   ├── stylera.js
│   │   │   │   └── xemoz.js
│   │   │   ├── sharedAPIs/
│   │   │   │   ├── apiMaintenance.js
│   │   │   │   ├── assertBinaryResponse.js
│   │   │   │   ├── detectApikeyIssue.js
│   │   │   │   ├── getByPath.js
│   │   │   │   ├── resolveDataResult.js
│   │   │   │   ├── resolveJsonResult.js
│   │   │   │   ├── resolveTextResult.js
│   │   │   │   ├── toBuffer.js
│   │   │   │   └── wrapAbort.js
│   │   │   └── importAPIs.js
│   │   ├── localProviders/
│   │   │   ├── randomFetchs/
│   │   │   │   ├── randomImageFetchs/
│   │   │   │   │   ├── alyaKujouFetchs/
│   │   │   │   │   │   ├── alyaKujou.json
│   │   │   │   │   │   └── getRandomImageAlyaKujou.js
│   │   │   │   │   ├── anzuHanashiroFetchs/
│   │   │   │   │   │   ├── anzuHanashiro.json
│   │   │   │   │   │   └── getRandomImageAnzuHanashiro.js
│   │   │   │   │   ├── elainaFetchs/
│   │   │   │   │   │   ├── elaina.json
│   │   │   │   │   │   └── getRandomImageElaina.js
│   │   │   │   │   ├── kurumiTokisakiFetchs/
│   │   │   │   │   │   ├── getRandomImageKurumiTokisaki.js
│   │   │   │   │   │   └── kurumiTokisaki.json
│   │   │   │   │   ├── mahiruShiinaFetchs/
│   │   │   │   │   │   ├── getRandomImageMahiruShiina.js
│   │   │   │   │   │   └── mahiruShiina.json
│   │   │   │   │   ├── mashaKujouFetchs/
│   │   │   │   │   │   ├── getRandomImageMashaKujou.js
│   │   │   │   │   │   └── mashaKujou.json
│   │   │   │   │   ├── micchonShikimoriFetchs/
│   │   │   │   │   │   ├── getRandomImageMicchonShikimori.js
│   │   │   │   │   │   └── micchonShikimori.json
│   │   │   │   │   ├── mikasaAckermanFetchs/
│   │   │   │   │   │   ├── getRandomImageMikasaAckerman.js
│   │   │   │   │   │   └── mikasaAckerman.json
│   │   │   │   │   ├── mikuNakanoFetchs/
│   │   │   │   │   │   ├── getRandomImageMikuNakano.js
│   │   │   │   │   │   └── mikuNakano.json
│   │   │   │   │   ├── mikuSakuraFetchs/
│   │   │   │   │   │   ├── getRandomImageMikuSakura.js
│   │   │   │   │   │   └── mikuSakura.json
│   │   │   │   │   ├── okusoraAyaneFetchs/
│   │   │   │   │   │   ├── getRandomImageOkusoraAyane.js
│   │   │   │   │   │   └── okusoraAyane.json
│   │   │   │   │   ├── rinNanakuraFetchs/
│   │   │   │   │   │   ├── getRandomImageRinNanakura.js
│   │   │   │   │   │   └── rinNanakura.json
│   │   │   │   │   ├── waguriKaokuroFetchs/
│   │   │   │   │   │   ├── getRandomImageWaguriKaokuro.js
│   │   │   │   │   │   └── waguriKaokuro.json
│   │   │   │   │   ├── yukiSuouFetchs/
│   │   │   │   │   │   ├── getRandomImageYukiSuou.js
│   │   │   │   │   │   └── yukiSuou.json
│   │   │   │   │   └── importRandomImageFetchs.js
│   │   │   │   ├── sharedRandom/
│   │   │   │   │   └── getRandomImageFromJson.js
│   │   │   │   └── importRandomFetchs.js
│   │   │   └── importLocalProviders.js
│   │   ├── scrapers/
│   │   └── importProviders.js
│   ├── quotes/
│   │   ├── buildQuotesMessage/
│   │   │   ├── quotedAccessExpired.js
│   │   │   ├── quotedAdminDemote.js
│   │   │   ├── quotedAdminPromote.js
│   │   │   ├── quotedAfkBack.js
│   │   │   ├── quotedAfkNotify.js
│   │   │   ├── quotedAiChat.js
│   │   │   ├── quotedApiError.js
│   │   │   ├── quotedBye.js
│   │   │   ├── quotedContact.js
│   │   │   ├── quotedDevFailed.js
│   │   │   ├── quotedDevRetry.js
│   │   │   ├── quotedFailed.js
│   │   │   ├── quotedGroupPic.js
│   │   │   ├── quotedGroupSettings.js
│   │   │   ├── quotedJoinRequest.js
│   │   │   ├── quotedMemberAdd.js
│   │   │   ├── quotedMemberRemove.js
│   │   │   ├── quotedModeFilter.js
│   │   │   ├── quotedModeReset.js
│   │   │   ├── quotedNoDelete.js
│   │   │   ├── quotedNoSpam.js
│   │   │   ├── quotedObfuscate.js
│   │   │   ├── quotedRandomPhoto.js
│   │   │   ├── quotedRemainingAccess.js
│   │   │   ├── quotedResultSticker.js
│   │   │   ├── quotedRetry.js
│   │   │   ├── quotedShalat.js
│   │   │   └── quotedWelcome.js
│   │   ├── sharedQuotes/
│   │   │   ├── buildContactQuotes.js
│   │   │   ├── buildImageQuotes.js
│   │   │   ├── buildPollQuotes.js
│   │   │   └── buildStickerQuotes.js
│   │   └── importQuotes.js
│   ├── tools/
│   │   ├── fonts/
│   │   │   ├── customFonts/
│   │   │   │   ├── sansBold.js
│   │   │   │   └── sansSoft.js
│   │   │   ├── importedFonts/
│   │   │   ├── sharedFonts/
│   │   │   │   ├── matchGlyph.js
│   │   │   │   └── sourceAlphabet.js
│   │   │   └── importFonts.js
│   │   ├── frameworkHTML/
│   │   │   ├── pingHtml/
│   │   │   │   ├── pingRoot/
│   │   │   │   │   ├── indexPing.html
│   │   │   │   │   ├── scriptPing.js
│   │   │   │   │   └── stylePing.css
│   │   │   │   ├── pingStats/
│   │   │   │   │   ├── cpuLoad.js
│   │   │   │   │   └── memoryLimit.js
│   │   │   │   └── mergePingHtml.js
│   │   │   └── importFrameworkHTML.js
│   │   ├── mediaTools/
│   │   │   ├── gifs/
│   │   │   │   ├── convertToGif.js
│   │   │   │   └── fetchGif.js
│   │   │   ├── toStickers/
│   │   │   │   ├── sharedToStickers/
│   │   │   │   │   ├── buildExif.js
│   │   │   │   │   └── stickerConvert.js
│   │   │   │   ├── writeExifImg.js
│   │   │   │   ├── writeExifRaw.js
│   │   │   │   └── writeExifVid.js
│   │   │   ├── voicenotes/
│   │   │   │   └── fetchVoiceNote.js
│   │   │   └── importMediaTools.js
│   │   ├── prompts/
│   │   │   ├── imagePrompts/
│   │   │   │   ├── getImgPrompts/
│   │   │   │   │   ├── toCarPortraitProm.js
│   │   │   │   │   ├── toSdProm.js
│   │   │   │   │   ├── toSmaProm.js
│   │   │   │   │   ├── toSmpProm.js
│   │   │   │   │   ├── toUrbanStreetProm.js
│   │   │   │   │   ├── toVogueProm.js
│   │   │   │   │   └── toWhiteHairProm.js
│   │   │   │   └── importImagePrompts.js
│   │   │   └── importPrompts.js
│   │   ├── timeLine/
│   │   │   ├── sharedTimeLine/
│   │   │   │   ├── clock.js
│   │   │   │   ├── date.js
│   │   │   │   ├── formatDuration.js
│   │   │   │   └── time.js
│   │   │   └── importTimeLine.js
│   │   ├── transformCase/
│   │   │   ├── sharedTransformCase/
│   │   │   │   └── textGuard.js
│   │   │   ├── transformText/
│   │   │   │   ├── toLowerFirst.js
│   │   │   │   ├── toLowerFirstAt.js
│   │   │   │   ├── toTitleCase.js
│   │   │   │   ├── toUpperFirst.js
│   │   │   │   └── toUpperFirstAt.js
│   │   │   └── importTransformCase.js
│   │   └── importTools.js
│   ├── upload/
│   │   ├── styleraUploader.js
│   │   └── uguu.js
│   └── exports.js
├── media/
│   └── image.png.zip
├── plugins/
│   ├── ai/
│   │   ├── ai.js
│   │   ├── bard.js
│   │   ├── blackbox.js
│   │   ├── claude.js
│   │   ├── copilot.js
│   │   ├── deep.js
│   │   ├── deepseek.js
│   │   ├── deepseekv2.js
│   │   ├── dolphin.js
│   │   ├── edubrain.js
│   │   ├── felo.js
│   │   ├── flux.js
│   │   ├── freegen.js
│   │   ├── gemini.js
│   │   ├── gita.js
│   │   ├── gpt4o.js
│   │   ├── gptfree.js
│   │   ├── haiku.js
│   │   ├── hd.js
│   │   ├── hdv2.js
│   │   ├── hdv3.js
│   │   ├── hdv4.js
│   │   ├── hdvid.js
│   │   ├── ideogram.js
│   │   ├── islam.js
│   │   ├── jeeves.js
│   │   ├── muslim.js
│   │   ├── nanobanana.js
│   │   ├── notrack.js
│   │   ├── overchat.js
│   │   ├── powerbrain.js
│   │   ├── public.js
│   │   ├── quillbot.js
│   │   ├── qwen.js
│   │   ├── realtime.js
│   │   ├── sufrsense.js
│   │   ├── text2img.js
│   │   ├── toanime.js
│   │   ├── tobabi.js
│   │   ├── toblonde.js
│   │   ├── toblur.js
│   │   ├── tobotak.js
│   │   ├── tobrewok.js
│   │   ├── tocar.js
│   │   ├── tochibi.js
│   │   ├── todpr.js
│   │   ├── todubai.js
│   │   ├── tofigura.js
│   │   ├── tofigurav2.js
│   │   ├── tofigurav3.js
│   │   ├── toghibli.js
│   │   ├── tohijab.js
│   │   ├── tohitam.js
│   │   ├── tojapanese.js
│   │   ├── tojepang.js
│   │   ├── tokacamata.js
│   │   ├── tokamboja.js
│   │   ├── tolego.js
│   │   ├── toliquor.js
│   │   ├── tomaid.js
│   │   ├── tomangu.js
│   │   ├── tomaya.js
│   │   ├── tomekah.js
│   │   ├── tomirror.js
│   │   ├── tomoai.js
│   │   ├── tomonyet.js
│   │   ├── topacar.js
│   │   ├── topacarv2.js
│   │   ├── topeci.js
│   │   ├── topenjabat.js
│   │   ├── topiramida.js
│   │   ├── topolaroid.js
│   │   ├── topunk.js
│   │   ├── toputih.js
│   │   ├── toreal.js
│   │   ├── toroblox.js
│   │   ├── toroh.js
│   │   ├── tosad.js
│   │   ├── tosatan.js
│   │   ├── tosd.js
│   │   ├── tosdmtinggi.js
│   │   ├── tosingapura.js
│   │   ├── tosma.js
│   │   ├── tosmp.js
│   │   ├── tostreetwear.js
│   │   ├── totato.js
│   │   ├── totrain.js
│   │   ├── totua.js
│   │   ├── toturky.js
│   │   ├── tounderground.js
│   │   ├── tourbanstreet.js
│   │   ├── toviking.js
│   │   ├── tovintage.js
│   │   ├── tovogue.js
│   │   ├── towhite.js
│   │   ├── tozombie.js
│   │   └── wormgpt.js
│   ├── dev/
│   │   ├── addplugin.js
│   │   ├── backup.js
│   │   ├── cekerror.js
│   │   ├── delplugin.js
│   │   ├── devmode.js
│   │   ├── findplugin.js
│   │   ├── getMsg.js
│   │   ├── getnamebot.js
│   │   ├── getplugin.js
│   │   ├── getppbot.js
│   │   ├── install.js
│   │   ├── merge.js
│   │   ├── obfuscate.js
│   │   ├── openplugin.js
│   │   ├── restart.js
│   │   ├── setnamebot.js
│   │   ├── setppbot.js
│   │   ├── tree.js
│   │   ├── uninstall.js
│   │   ├── unlockgc.js
│   │   └── update.js
│   ├── group/
│   │   ├── add.js
│   │   ├── afk.js
│   │   ├── closegc.js
│   │   ├── delete.js
│   │   ├── demote.js
│   │   ├── gcmode.js
│   │   ├── getdeskgc.js
│   │   ├── getidgc.js
│   │   ├── getlinkgc.js
│   │   ├── getnamegc.js
│   │   ├── getppgc.js
│   │   ├── hidetag.js
│   │   ├── kick.js
│   │   ├── listadmin.js
│   │   ├── listall.js
│   │   ├── listmember.js
│   │   ├── opengc.js
│   │   ├── pin.js
│   │   ├── promote.js
│   │   ├── resetcachegroup.js
│   │   ├── revokelinkgc.js
│   │   ├── setbye.js
│   │   ├── setdeskgc.js
│   │   ├── setnamegc.js
│   │   ├── setppgc.js
│   │   ├── setwelcome.js
│   │   └── upswgc.js
│   ├── main/
│   │   ├── daftar.js
│   │   ├── daily.js
│   │   ├── menu.js
│   │   ├── peraturan.js
│   │   └── tutorial.js
│   ├── maker/
│   │   ├── afinitasml.js
│   │   ├── afinitasmlv2.js
│   │   ├── artemis.js
│   │   ├── avenger.js
│   │   ├── balago.js
│   │   ├── basket.js
│   │   ├── batman.js
│   │   ├── beautiful.js
│   │   ├── blackpink2.js
│   │   ├── blood.js
│   │   ├── boom.js
│   │   ├── branding.js
│   │   ├── breakwall.js
│   │   ├── cake.js
│   │   ├── carbon.js
│   │   ├── cbadminton.js
│   │   ├── clouds.js
│   │   ├── deadpool.js
│   │   ├── devil.js
│   │   ├── dragonball.js
│   │   ├── drake.js
│   │   ├── eraser.js
│   │   ├── fakedana.js
│   │   ├── fakedev.js
│   │   ├── fakeff.js
│   │   ├── fakeffduo.js
│   │   ├── fakeffv2.js
│   │   ├── fakegopay.js
│   │   ├── fakeml.js
│   │   ├── fakengl.js
│   │   ├── fakeovo.js
│   │   ├── fakeseabank.js
│   │   ├── flames.js
│   │   ├── girl.js
│   │   ├── glasses.js
│   │   ├── glitchtext.js
│   │   ├── glow.js
│   │   ├── gradient.js
│   │   ├── grass.js
│   │   ├── igc.js
│   │   ├── iqc.js
│   │   ├── iqcdark.js
│   │   ├── iqcg.js
│   │   ├── iqcimg.js
│   │   ├── iqcpink.js
│   │   ├── iqcv2.js
│   │   ├── iqs.js
│   │   ├── iqw.js
│   │   ├── joker.js
│   │   ├── lifebuoys.js
│   │   ├── lines.js
│   │   ├── magma.js
│   │   ├── marvel.js
│   │   ├── matrix.js
│   │   ├── multicolor.js
│   │   ├── music.js
│   │   ├── naruto.js
│   │   ├── neon.js
│   │   ├── nulis.js
│   │   ├── pakustadz.js
│   │   ├── papercut.js
│   │   ├── pig.js
│   │   ├── pornhub.js
│   │   ├── puppy.js
│   │   ├── quotes.js
│   │   ├── quoteslaptop.js
│   │   ├── sand.js
│   │   ├── shadow.js
│   │   ├── slice.js
│   │   ├── sliced.js
│   │   ├── sunset.js
│   │   ├── thor.js
│   │   ├── thunder.js
│   │   ├── tosketch.js
│   │   ├── towasted.js
│   │   ├── transformer.js
│   │   ├── twobuttons.js
│   │   ├── typography.js
│   │   └── valentine.js
│   ├── random/
│   │   ├── alyaKujou.js
│   │   ├── anzuHanashiro.js
│   │   ├── elaina.js
│   │   ├── kurumiTokisaki.js
│   │   ├── mahiruShiina.js
│   │   ├── mashaKujou.js
│   │   ├── micchonShikimori.js
│   │   ├── mikasaAckerman.js
│   │   ├── mikuNakano.js
│   │   ├── mikuSakura.js
│   │   ├── okusoraAyane.js
│   │   ├── rinNanakura.js
│   │   ├── waguriKaokuro.js
│   │   └── yukiSuou.js
│   ├── sticker/
│   │   ├── attp.js
│   │   ├── brat.js
│   │   ├── bratanimev2.js
│   │   ├── bratbahlil.js
│   │   ├── bratbearnad.js
│   │   ├── bratcewe.js
│   │   ├── bratchika.js
│   │   ├── bratdoraemon.js
│   │   ├── bratelaina.js
│   │   ├── bratgojo.js
│   │   ├── bratgura.js
│   │   ├── brathd.js
│   │   ├── brathellokitty.js
│   │   ├── bratkobato.js
│   │   ├── bratmegawati.js
│   │   ├── bratmenhera.js
│   │   ├── bratmika.js
│   │   ├── bratnezuko.js
│   │   ├── bratprobowo.js
│   │   ├── bratqiqi.js
│   │   ├── bratruromiya.js
│   │   ├── bratsinchan.js
│   │   ├── bratsquidward.js
│   │   ├── bratvid.js
│   │   ├── bratvidhd.js
│   │   ├── jarvismeme.js
│   │   ├── quotely.js
│   │   ├── smeme.js
│   │   ├── sticker.js
│   │   ├── stickerv2.js
│   │   ├── ttp.js
│   │   └── watermark.js
│   ├── tools/
│   │   ├── idch.js
│   │   ├── idgc.js
│   │   └── ping.js
│   └── upload/
│       ├── upStylera.js
│       └── upUguu.js
├── handler.js
├── index.js
├── LICENSE.md
├── package.json
└── README.md
```

</details>

## 🏗️ Architecture

```mermaid
flowchart LR
    A[WhatsApp message] --> B[index.js<br/>Baileys connection]
    B --> C[handler.js<br/>serialize + parse prefix]
    C --> D{Access checks<br/>group / admin / dev / limit}
    D -- denied --> E[Denial reply]
    D -- allowed --> F[runPlugin.js<br/>timeout + error handling]
    F --> G[plugins/*<br/>command handler]
    G --> H[library helpers<br/>databases, providers, media]
    G --> I[Reply to chat]
    J[hotReload.js] -. watches .-> G
```

## 🔧 Configuration

Settings live in `library/modules/adjustables/configs/`. Each file sets one `global.*` object that the rest of the code reads.

| File | Purpose |
|------|---------|
| `globalBot.js` | Bot name, WhatsApp number, session name, database names, pairing mode, and prefix |
| `globalDev.js` | Developer numbers and developer-only settings |
| `globalUser.js` | User defaults, limits, and registration settings |
| `globalMedia.js` | Remote asset URLs (png, mp4, mp3) used across plugins |
| `globalApi.js` | API provider settings |
| `globalTime.js` | Time zone label used in logs and replies |
| `globalInterval.js`, `globalTTL.js` | Timers and cache lifetimes |
| `globalSchedule.js`, `globalShalat.js` | Scheduled messages and prayer-time features |
| `globalMessage.js`, `globalGroupText.js`, `globalEventMsg.js` | Reply texts and group event messages |
| `globalPackname.js`, `globalWebsite.js`, `globalSosial.js` | Sticker pack info, website, and social links |
| `globalFallback.js`, `globalExclude.js` | Fallback values and paths excluded from searches |

> **Security:** do not commit real phone numbers, pairing codes, API keys, or session files. Clear these values before pushing to a public repository.

## 🧩 Creating a Plugin

Each plugin is a single ESM file in `plugins/<category>/` that exports a default handler function. Use the existing plugins as your reference.

### Minimal example

Based on `plugins/group/getlinkgc.js`:

```js
let handler = async (m, { conn }) => {
  const { success } = global?.mapEmoji || {}

  const code = await conn.groupInviteCode(m.chat)
  const link = `https://chat.whatsapp.com/${code}`

  await conn.sendMessage(m.chat, {
    text: `${success} \`Group link retrieved\``,
    footer: "⤹ Click to Copy",
    nativeFlow: [
      {
        name: "cta_copy",
        buttonParamsJson: JSON.stringify({
          display_text: "copy",
          id: "copy_gc_link",
          copy_code: link
        })
      }
    ]
  }, { quoted: global?.EventMsg })
}

handler.command = ["getlinkgc", "linkgc"]
handler.tags = ["group"]
handler.help = ["getlinkgc", "linkgc"]
handler.group = true
handler.admin = true
handler.botAdmin = true

export default handler
```

### Rules

- **`handler.command`**: array of trigger words, written as an explicit array literal.
- **`handler.tags`**: the category shown in the menu, matching the folder name.
- **`handler.help`**: array of help entries shown in the menu, written as an explicit array literal.
- **Access flags** (all optional):
  - `group`: group chats only.
  - `private`: private chats only.
  - `admin`: group admins only.
  - `botAdmin`: the bot must be a group admin.
  - `dev`: developers only.
  - `register`: user must be registered.
  - `limit`: consumes usage limit when the command runs.
- **Follow existing patterns.** Reuse helpers from `library/exports.js` instead of writing your own versions of them.
- **Media helpers** cache fetched buffers in memory until restart (for example `fetchVnBuffer` in `library/modules/media.js`). Reuse them to avoid repeated downloads.
- **Voice notes** must be converted to opus/ogg before sending (`toPTT()`). Use `audio/ogg; codecs=opus` as the mimetype.

## 🛠️ Tech Stack

- **Runtime:** Node.js 24+ (ESM)
- **WhatsApp:** `@rexxhayanasi/elaina-baileys`
- **Media:** `sharp`, `canvas`, `fluent-ffmpeg`, `@ffmpeg-installer/ffmpeg`, `node-webpmux`
- **Networking and parsing:** `axios`, `node-fetch`, `form-data`, `cheerio`
- **Utilities:** `chalk`, `pino`, `fs-extra`, `archiver`, `qrcode-terminal`, `javascript-obfuscator`

## 🗺️ Roadmap

- [x] Release version 1.0
- [x] Add multi-language support
- [ ] Integrate with third-party APIs
- [ ] Offline mode

See the [open issues](https://github.com/username/repo/issues) for the full list of proposed features.

## 🤝 Contributing

Contributions are welcome. Follow these steps:

1. Fork the project.
2. Create a feature branch (`git checkout -b feature/NewFeature`).
3. Commit your changes (`git commit -m 'Add NewFeature'`).
4. Push to the branch (`git push origin feature/NewFeature`).
5. Open a Pull Request.

Read [CONTRIBUTING.md](CONTRIBUTING.md) for the full guide.

## ❓ FAQ

<details>
<summary>Is this project free to use?</summary>

Yes. The project is open source under the MIT License. See [`LICENSE.md`](LICENSE.md).

</details>

<details>
<summary>How do I report a bug?</summary>

Open the [Issues](https://github.com/username/repo/issues) tab and create a new report with clear details.

</details>

<details>
<summary>Why does the bot not respond to commands?</summary>

Check that the prefix matches `globalBot.js`, that the session is still linked, and that the command's access flags (group, admin, dev, and so on) are satisfied.

</details>

## 📄 License

Distributed under the MIT License. See [`LICENSE.md`](LICENSE.md) for details.

## 📬 Contact

**Your Name** - [@twitter_handle](https://twitter.com/handle) - email@example.com

Project Link: [https://github.com/username/repo](https://github.com/username/repo)

## 🙏 Acknowledgements

- [Baileys / elaina-baileys](https://github.com/WhiskeySockets/Baileys)
- [Sharp](https://github.com/lovell/sharp)
- [FFmpeg](https://ffmpeg.org/)
- All contributors who helped build this project 🎉

---

<div align="center">

⭐ If this project helps you, please give it a **star**!

</div>
