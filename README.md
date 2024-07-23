# Discord Player YouTubei

This is a preview the v7 version of the YouTube system that discord-player will be using made backwards compatiable with v6.

## Installation

```bash
$ npm install discord-player-youtubei
# ----------- or -----------
$ yarn add discord-player-youtubei
```

## Usage

#### Typescript and ESM

```ts
import { YoutubeiExtractor } from "discord-player-youtubei"

const player = useMainPlayer() // or new Player()

player.extractors.register(YoutubeiExtractor, {})
```

#### CommonJS

```ts
const { YoutubeiExtractor } = require("discord-player-youtubei")

const player = useMainPlayer() // or new Player()

player.extractors.register(YoutubeiExtractor, {})
```

*I have seem many people registering the extractor in their commands. DO NOT DO THIS*

## Signing into YouTube

First run the following command
```bash
$ npx --no discord-player-youtubei
```

The token will be printed out shortly

*In case of errors, you can directly run the `generateOauthTokens` function exported by discord-player-youtubei*

```ts
import { YoutubeiExtractor } from "discord-player-youtubei"

const player = useMainPlayer()
const oauthTokens = getOauthTokens() // The tokens printed from step above

player.extractors.register(YoutubeiExtractor, {
    authentication: oauthTokens
})
```

## Rotating your token

Since Youtube has a hard limt (which is not that strict), we can provide a rotator config when registering the extractor. View [Rotator](./Rotator.md)

## Options for YoutubeiExtractor

```ts
interface RotatorShardOptions {
	authentications: string[];
	rotationStrategy: "shard";
	currentShard: number;
}

interface RotatorRandomOptions {
	authentications: string[];
	rotationStrategy: "random";
}

type RotatorConfig = RotatorShardOptions | RotatorRandomOptions

interface YoutubeiOptions {
	authentication?: string;
	overrideDownloadOptions?: DownloadOptions;
	createStream?: (q: Track, extractor: BaseExtractor<object>) => Promise<string | Readable>;
	signOutOnDeactive?: boolean;
	streamOptions?: {
		useClient?: InnerTubeClient
	};
	rotator?: RotatorConfig
}
```

### Notice Regarding YouTube Streaming

Streaming from YouTube is against their Terms of Service (ToS). Refer to [`LEGAL.md`](./LEGAL.md) to view the risks using YouTube.
