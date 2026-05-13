# update_widget_settings

Updates General + Guest settings via `PUT /ClientBotSettings`. Send ONLY the fields you want to change — backend loads current state from DB and applies your values on top (omitted fields preserved).

{{> update_flow}}

## General > Visibility

- `enableUserProfile` (bool) — show widget to registered customers
- `enableVisitorProfile` (bool) — show widget to guests
- `isLevelCardVisible` (bool) — show VIP tiers card
- `enableLeaderboard` (bool) — show leaderboard tab
- `enableLevelBenefits` (bool) — show recent tiers benefits
- `enableAllGamesPage` (bool) — show all games page
- `enableCalendarCampaignCard` (bool) — show calendar campaign card
- `isReferralRewardCardVisible` (bool) — show referral reward card
- `isReferralPointsVisible` (bool) — show referral points
- `enableNotifications` (bool) — show notifications
- `enableFAQ` (bool) — show FAQ section
- `enableGBFooter` (bool) — show "Powered by Gameball" footer
- `isCouponTabVisible` (bool) — show coupons tab
- `isWalletPointsVisible` (bool) — show wallet points card
- `isRankPointsVisible` (bool) — show rank/score points card
- `isPointsExpiryVisible` (bool) — show expiring points warning
- `enableFamilyWallet` (bool) — enable family wallet
- `enableGuestReward` (bool) — enable guest rewards
- `enableAchievements` (bool) — show achievements
- `widgetReferralIcon` — referral icon: `null` = default icon, `"none"` = no image, URL = custom uploaded image

## Branding > Guest

- `widgetTrophyIcon` — guest trophy icon: `null` = default, `"none"` = no image, URL = custom
- `buttonLink` (URL) — guest launcher button link
- `signinLink` (URL) — guest sign-in/signup link

## Branding > Identity (icons saved via main PUT)

- `earnIconUrl` (URL) — earn section icon
- `redeemIconUrl` (URL) — redeem section icon
- `gamesBannerImageUrl` (URL) — games banner background
- `calendarBannerBackgroundUrl` (URL) — calendar card background
- `calendarBannerIconUrl` (URL) — calendar card icon

## Referral

- `isReferralOn` (bool) — enable referral program
- `referralSignUpLink` (URL) — referral signup link
- `referralSharingOption` (int) — `1`=Link, `2`=Code

## Display

- `defaultTab` (int) — default tab when widget opens
- `programName` (string) — loyalty program name
- `rankPointsName` (string) — custom name for rank/score points
- `walletPointsName` (string) — custom name for wallet points
- `welcomeMessage` (string) — welcome message for guests
- `offlineStatemessage` (string) — offline state message
- `button` (string) — guest launcher button text

## Image / icon source

For URL fields above, get icons from `get_icons` (library) or upload via `utilsApi.uploadImage`.
