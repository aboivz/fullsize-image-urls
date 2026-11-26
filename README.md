# Full-size image URL cheat sheet

Most sites show a resized copy of each image and keep a larger file at a nearly identical address. This table lists, per site, what the thumbnail address looks like and the edit that gets you the full-size file. Where a row gives a date, I checked it against the live image server on that day. Sites change their CDNs, so any row can go stale; if one stops working, please open an issue or send a pull request.

Example addresses are shortened with `…` where an ID is long. The part you edit is always shown in full.

## Marketplaces

| Site | Thumbnail URL looks like | Change | Result (measured, date) |
|---|---|---|---|
| Amazon | `m.media-amazon.com/images/I/71abc._AC_SX300_SY300_.jpg` | Delete the size code between the image ID and the extension: `…/I/71abc.jpg` | Page copy 342 px wide, upload 2560x2560 with its white margin (2026-11-01, rechecked 2026-11-09) |
| AliExpress | `ae-pic-a1.aliexpress-media.com/kf/Sabc.jpg_480x480q75.jpg_.avif` | Delete everything after the first `.jpg`: `…/kf/Sabc.jpg` | 480x480 AVIF thumbnails became 800x800 or 1000x1000 photos on 11 listings; Chrome receives them as WebP (2026-11-11) |
| Taobao, 1688 | `img.alicdn.com/imgextra/i1/123/O1CN01.jpg_220x220q90.jpg` | Delete everything after the first `.jpg`: `…/O1CN01.jpg` | |
| Taobao search tiles | `img.alicdn.com/bao/uploaded/i3/1618450690/O1CN01H1GP…~crop,130,0,540,540~_!!1618450690.png` | Delete `~crop,130,0,540,540~`: `…/O1CN01H1GP…_!!1618450690.png` | 800x540 uncropped file instead of the 540x540 crop (2026-10-24) |
| Shopee | `down-vn.img.susercontent.com/file/vn-11134207-abc@resize_w164_nl.webp`, or `…/vn-11134207-abc_tn` | Delete `@resize_…`, `_tn` and `.webp` so the path ends at the file ID | 320x320 WebP became a 1024x1024 JPEG of 867 KB; keeping `.webp` gives the same size as WebP (2026-11-16) |
| Lazada | `img.lazcdn.com/us/domino/abc.jpg_2200x2200q80.jpg_.avif` (also `slatic.net`) | Delete everything after the first `.jpg` | An `_80x80q80.jpg` copy became a 1000x1000 JPEG; a PNG upload stayed PNG at 1254x1254 (2026-11-16) |
| Tiki | `salt.tikicdn.com/cache/100x100/ts/category/ed/20/60/afa.png.webp` | Delete `/cache/100x100` and the trailing `.webp`: `…/ts/category/ed/20/60/afa.png` | 280x280 copies became 800x800 and 1000x1000 on two products (2026-11-16) |
| TikTok Shop | `p16-oec-sg.ibyteimg.com/…/6fa9~tplv-aphluv4xwc-resize-webp:260:260.webp` | Keep `~tplv-<code>`, replace the rest with `-origin-jpeg.jpeg`, drop any query | Full pixel size on all 45 photos I fetched, 390x520 to 5906x5906; `-origin-image.image` returns the stored format instead (2026-11-01). The US shop host `p16-oec-general-useast5.ttcdn-us.com` takes the same edit: 8 of 8 swaps returned 200 without a signature (2026-11-22) |
| Shein | `img.ltwebstatic.com/v4/j/spmp/2026/09/21/09/1789abc_thumbnail_405x552.jpg` (or `_thumbnail_900x.webp`) | Delete `_thumbnail_<size>` and end the name in `.jpg` (PNG files keep `.png`) | A 405x539 copy became 1340x1785; 27 photos ranged from 913x913 to 2200x2200 (2026-11-01) |
| Temu | `img.kwcdn.com/product/open/…-goods.jpeg?imageView2/2/w/264/q/70/format/avif` | Delete the query (`?imageView2/…` or `?imageMogr2/…`) | A 264x264 AVIF became a 1600x1600 JPEG; 18 stored files ran from 800x800 to 3200x3200 (2026-11-01) |
| eBay | `i.ebayimg.com/images/g/abc/s-l225.jpg` | Change the number to `s-l1600` | 1600x1600, 1600x1429 and 1017x725; eBay caps the long side at 1600 and does not enlarge (2026-10-29) |
| Etsy | `i.etsystatic.com/123/r/il/abc/456/il_340x270.456_xyz.jpg` (or `il_794xN`) | Replace the size with `il_fullxfull` | The uploaded photo (2026-10-25) |
| Poshmark | `di2ponv0v5otw.cloudfront.net/posts/2026/09/18/6aadc2d2…/s_6aadc373….jpg` (or `m_`) | Change the `s_` or `m_` prefix to `l_` | `l_` is 1000 px wide: 1000x1000 or 1000x1333 on ten listings. With no prefix at all you get the seller's upload, 768 to 1600 px wide in that sample (2026-11-13) |
| Depop | `media-photos.depop.com/b1/39247988/2066921891_32f7…/P6.jpg` | Change `P<n>` to `P0` | `P6` is 480 px, `P0` 1280 px on the photos I checked (2026-10-24) |
| Mercari Japan | `static.mercdn.net/thumb/item/webp/m78136360600_1.jpg`, or `…/c!/w=240,f=webp/thumb/photos/m80772985421_1.jpg` | Replace everything before the file name with `/item/detail/orig/photos/` | Checked 2026-10-24 |
| Mercari US | `u-mercari-images.mercdn.net/photos/m47216877271_1.jpg?width=200&height=200` | Delete `?width` and `?height` | The bare address gave 1600x1600. A larger `width` is scaled up: `?width=8000` returned 8000x8000 (2026-11-22) |
| Mercado Libre | `http2.mlstatic.com/D_Q_NP_744852-MLA110348873558_052026-V.webp` | Use the prefix `D_NQ_NP_` and the size letters `-OO`; drop `2X_` and any product name after the size letters | A 320x320 square became 750x1200; 51 photos ranged from 350x257 to 1250x1918. `D_Q_NP_` with `-OO` pads the photo to a 1920x1920 square (2026-11-01, rechecked 2026-11-14) |
| Flipkart | `rukminim2.flixcart.com/image/612/612/xif0q/shoe/x/u/k/6-klunys….jpeg?q=70` | Delete the two numbers after `/image/` and the query | 25 photos came back as the stored JPEG, 627x759 to 3584x4800; bigger numbers only upscale (2026-11-01) |
| Coupang | `thumbnail10.coupangcdn.com/thumbnails/remote/230x230ex/image/vendor_inventory/15a4/d514….jpg` | Change the host to `image10.coupangcdn.com` and delete `/thumbnails/remote/230x230ex` | Checked 2026-10-24 |
| Rakuten | `thumbnail.image.rakuten.co.jp/@0_mall/topgift/cabinet/g24444.jpg?_ex=128x128`, or `tshop.r10s.jp/adidas/cabinet/p2/gy8257_l.jpg?fitin=275:275` | Use the host `image.rakuten.co.jp`, delete `/@0_mall` and the query | Checked 2026-10-24 |
| Tokopedia | `images.tokopedia.net/img/cache/500-square/hDjmkQ/2021/9/20/987b….jpg.webp?ect=4g` | Delete `/cache/500-square`, the trailing `.webp` and the query | Checked 2026-10-24 |
| Naver Shopping | `shop-phinf.pstatic.net/20180611_179/…/5200….png?type=f300` (also `shopping-phinf`) | Delete `?type=…`; `type=o1000` upscales | Checked 2026-10-24 |
| Allegro | `a.allegroimg.com/s180x180/1e0322/3489f389…` (also `s360`, `s720`) | Replace the size folder with `original` | Checked 2026-10-24 |
| Grailed | `media-assets.grailed.com/prd/listing/39364952/7e70105b…?w=240` | Delete the query | `w=5000` returns the same file as the bare address (2026-10-24) |

## Retailers and brands

| Site | Thumbnail URL looks like | Change | Result (measured, date) |
|---|---|---|---|
| Walmart | `i5.walmartimages.com/seo/<name>_8097d32f….jpeg?odnHeight=180&odnWidth=180&odnBg=FFFFFF` | Set `?odnHeight=4000&odnWidth=4000&odnBg=FFFFFF` | The upload byte for byte on 32 products, 1000x1000 to 3756x3805: the JPEG size matched the server's `x-tb-optimization-original-content-size` header, and nothing was upscaled. Deleting the `odn…` parameters gives the full pixel size but a re-compressed AVIF, about a third of the bytes (2026-11-22) |
| Target | `target.scene7.com/is/image/Target/GUEST_0c1486db…?wid=300&hei=300&qlt=80&fmt=webp` | Delete `wid` and `hei`, add `scl=1` | Stored size on 29 photos, 500x500 to 3984x3984; a larger `wid` upscales (2026-10-31) |
| Best Buy | `pisces.bbystatic.com/image2/BestBuy_US/images/products/6505/6505727_rd.jpg;maxHeight=256;maxWidth=384?format=webp` | Delete `;maxHeight=…;maxWidth=…` | 230x300 became 2265x2956; 38 photos ranged from 368x267 to 2787x3589. Chrome usually gets AVIF (2026-11-01) |
| Home Depot | `images.thdstatic.com/productImages/794dc46d…/svn/dewalt-power-drills-dcd794d1-64_400.jpg` | Change `_400` to `_1000` | `_1000` is the largest stored size; `_1500` and up return the same 1000 px file |
| Wayfair | `assets.wfcdn.com/im/09354923/resize-h755-w755%5Ecompr-r85/2222/222277958/Area+Rug.jpg` | Delete `resize-…%5E` (or `timg-…`, `scale-…`); keep `compr-r85` | 755x755 became 2000x2117; 27 of 33 photos came back larger, up to 6979x4823. Four returned a "No Image Available" placeholder (2026-11-01) |
| IKEA | `www.ikea.com/us/en/images/products/billy-bookcase-black-oak-effect__1097107_pe864733_s5.jpg?f=xxs` | Set `?f=g` (`xg` and `xxg` give the same file) | 2000x2000. With no `f` you get 1400 px, and `sg` is 1600. A plain request gets JPEG (the black oak BILLY is 992.8 KB), Chrome gets AVIF. 17 photos going back to 2008 had real detail at 2000, not an upscale (2026-11-23) |
| Zalando | `img01.ztat.net/article/spp-media-p1/00d4…/6413….jpg?imwidth=300` | Delete `imwidth`; keep `filter=` | Checked 2026-10-24 |
| H&M | `image.hm.com/assets/hm/03/5f/035f9de6….jpg?imwidth=256` | Delete `imwidth` | Checked 2026-10-24 |
| Sephora | `www.sephora.com/productimages/sku/s1966258-main-zoom.jpg?imwidth=375` | Delete `imwidth`; keep `pb=` | Checked 2026-10-24 |
| Macy's, Kohl's | `media.kohlsimg.com/is/image/kohls/1390818?wid=240&hei=240&op_sharpen=1`, or `slimages.macysassets.com/is/image/MCY/…/11488742_fpx.tif?wid=500&hei=613&fit=fit` | Set `wid=3000&hei=3000&fit=constrain,0` | Stored size up to 3000 px without upscaling; `scl=1` returns 403 on large Macy's uploads (2026-10-24) |
| Ulta | `media.ulta.com/i/ulta/2266731?w=720&h=720&fmt=webp` | Delete `w` and `h`; keep `fmt` and `$…$` presets | 2000 px master; a bigger `w` upscales (2026-10-24) |
| Nike | `static.nike.com/a/images/t_web_pw_592_v2/f_auto/u_9ddf04c7,…/1f87…/NIKE+PEGASUS.png` | Delete the size steps (`t_…`, `w_…`, `c_…`, `f_…`) after `/a/images/`; keep the `u_` background step | A 1070x1338 product photo became 2880x3600; a 1184x1184 category tile became 3144x3144 (2026-11-11) |
| adidas | `assets.adidas.com/images/w_600,f_auto,q_auto/1790130a…_9366/Grand_Court_01_standard.jpg` | Delete the size step after `/images/` | Checked 2026-10-24 |

## Social and photo sites

| Site | Thumbnail URL looks like | Change | Result (measured, date) |
|---|---|---|---|
| X (Twitter) | `pbs.twimg.com/media/Fabc?format=jpg&name=small` | Set `name=orig` | |
| Bluesky | `cdn.bsky.app/img/feed_thumbnail/plain/<did>/<cid>@jpeg` | Change `feed_thumbnail` to `feed_fullsize` | 1000x750 WebP became 4000x3000; add `@jpeg` or `@png` to the end to pick the format (2026-11-09) |
| Reddit | `preview.redd.it/fall-at-mount-rainier-v0-xmq07ebqcaxh1.jpeg?width=1080&…&s=abc` | Use the host `i.redd.it`, keep only the ID and extension, drop the query: `i.redd.it/xmq07ebqcaxh1.jpeg` | A 640x360 preview became 4000x2252 (2026-10-24) |
| Pinterest | `i.pinimg.com/236x/aa/bb/cc/abc.jpg` (also `474x`, `736x`) | Replace the size folder with `originals` | A 236x419 tile became 1080x1920. `originals` keeps the uploaded format: PNG and GIF pins return 403 at `.jpg`, so try `.png` then `.gif`, then `1200x` with `.jpg`. 3 of 6 pins needed this (2026-11-22) |
| Flickr | `live.staticflickr.com/65535/55601193566_be868554f4_n.jpg`, or no size letter | Change the size letter to `_b` | `_b` is 1024 px: a 400x267 thumbnail became 1024x683 (2026-11-10) |
| Behance | `mir-s3-cdn-cf.behance.net/projects/max_808_webp/abc.png` | Replace the size folder with `original` | Covers went from previews as small as 115x90 to files as large as 2498x3526 (2026-10-23) |
| Dribbble | `cdn.dribbble.com/userupload/123/file/original-abc.png?format=webp&resize=400x300&vertical=center` | Replace the query with `?format=jpg` (or `?format=png` for a PNG). With no query, Chrome gets a WebP copy | 400x300 WebP previews; the uploads were 1600x1200 to 6667x5000 on 21 shots (2026-11-12). Rechecked: a bare JPEG URL sent Chrome 760 KB of WebP, `?format=jpg` the 3.5 MB upload, identical to a plain request (2026-11-21) |
| Unsplash | `images.unsplash.com/photo-123?ixlib=rb-4.1.0&ixid=abc&w=400&q=60&auto=format&fit=crop` | Delete `w`, `h`, `fit`, `crop`, `q`, `dpr`, `auto`, `fm` and `cs` | 4878x3252 with no size parameters, 1920x1280 with `?w=1920` (2026-11-13) |
| Substack | `substackcdn.com/image/fetch/$s_!abc!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fabc_2048x1152.png` | Delete `w_1456,c_limit,` for the full pixel size. For the stored file, URL-decode everything after the last `/` and open that `substack-post-media.s3.amazonaws.com` address | The post shows at most 1456 px wide. With no `w_` a 2048x1152 image came back at full size but recompressed (412 KB JPEG); the decoded S3 file was the original 5.3 MB PNG. Only the S3 file kept the stored format on all 6 images from 3 public posts, and a larger `w_` never upscales (2026-11-22) |

## Site builders and store platforms

| Site | Thumbnail URL looks like | Change | Result (measured, date) |
|---|---|---|---|
| Shopify | `cdn.shopify.com/s/files/1/0001/products/shoe_600x.jpg?v=123`, or `<shop>/cdn/shop/files/bag_300x300@2x.webp?v=1&width=300` | Delete the size from the name (`_600x`, `_300x300@2x`, `_grande`, `_large` and so on) and the `width`, `height` and `crop` parameters | Checked 2026-10-23 |
| WordPress, WooCommerce | `<site>/wp-content/uploads/2024/01/photo-300x200.jpg` | Delete `-300x200`, `-scaled` or `-rotated` before the extension | A 600x600 gallery copy became 1600x1600; a `-scaled` 2211x2560 copy came from a 3864x4474 upload (2026-11-01) |
| Wix | `static.wixstatic.com/media/1e04d5_1b53…~mv2.jpg/v1/fill/w_550,h_550,al_c,q_80/1e04d5_1b53…~mv2.jpg` | Delete everything from `/v1/` on | A 960x1200 page copy came from a 2584x3230 upload, a 400x118 logo from a 1367x508 PNG (2026-11-01) |
| Squarespace | `images.squarespace-cdn.com/content/v1/5ce82b63…/1559253663317-EOSY…/brine.jpg?format=300w` | Delete `?format=…w` | The largest stored copy, at most 2500 px wide: a 3840x5760 upload came back at 2500x3750 (2026-11-01) |
| BigCommerce | `cdn11.bigcommerce.com/s-tbqmniv/images/stencil/500x659/products/1626/26788/AC.SK.CH19….jpg` (or `/stencil/1280w/`) | Replace the size folder with `original` | A 1280x1280 copy became 4359x4359; nothing was enlarged (2026-11-01) |
| Square Online | `60f1aead….cdn6.editmysite.com/uploads/b/…/2021-01-26_1611716357.jpg?width=400&optimize=medium&height=480&fit=cover` | Delete the query | Checked 2026-10-24 |
| Webflow | `cdn.prod.website-files.com/686294e2…/6a8e97f9…_home-source-bg-p-500.webp` | Delete `-p-500` (any `-p-<width>`) | On 56 images, every original was wider than the largest copy its page listed (2026-11-01) |
| VTEX stores | `arteli.vtexassets.com/arquivos/ids/201426-500-auto?v=…&width=500&height=auto&aspect=true` | Delete `-500-auto` from the path and the `width`, `height` and `aspect` parameters; an explicit `-2000-2000` upscales | Checked 2026-10-24 |

## Image CDNs

| Site | Thumbnail URL looks like | Change | Result (measured, date) |
|---|---|---|---|
| Cloudinary | `res.cloudinary.com/demo/image/upload/w_400,c_fill/q_auto/v1712/folder/shoe.jpg` | Delete the size, crop, quality and format steps between `/upload/` and the version. I leave URLs with `l_` or `u_` layers alone, since that is how sites add watermarks | |
| Contentful | `images.ctfassets.net/wowgx05xsdrr/121Tt…/5a01…/UPLIFT-Desk.jpg?w=300&h=200&fit=fill&fm=webp&q=75` | Delete the query | Checked 2026-10-24 |

## Other

| Site | Thumbnail URL looks like | Change | Result (measured, date) |
|---|---|---|---|
| Wikipedia, Wikimedia Commons | `upload.wikimedia.org/wikipedia/commons/thumb/a/ab/Cat.jpg/220px-Cat.jpg` (also `thumb.wikimedia.org`) | Delete `/thumb` and the last path part, drop the query, use the host `upload.wikimedia.org`: `…/commons/a/ab/Cat.jpg` | The Einstein portrait in the English article is 4530x5607 behind a 250 px thumbnail (2026-11-14) |
| Zillow | `photos.zillowstatic.com/fp/cce8b13b…-sr_576_384.webp` | Replace the suffix with `-uncropped_scaled_within_1536_1152.jpg` | 1536x1024 for a landscape photo, 793x1152 for a portrait one, whole frame. `-sc_1920_1280` is larger but crops portrait photos (2026-11-08) |

## How to use

1. Right-click the image and choose "Open image in new tab".
2. Edit the address as the table shows.
3. Press Enter and save the result.

Most rows are one of three edits: delete a size written into the file name (`-300x200`, `_600x`, `._AC_SX300_`, `_thumbnail_405x552`), swap a size folder in the path (`/236x/` to `/originals/`, `/stencil/500x659/` to `/stencil/original/`), or delete size parameters from the query (`?w=400`, `?imwidth=300`, `?format=300w`). Deleting the size usually beats typing a bigger one. On Target, Flipkart, Ulta, VTEX and Naver a bigger number returns an upscaled copy with no extra detail.

Several CDNs choose the format from what the browser says it accepts, so Chrome often receives WebP or AVIF even when the address ends in `.jpg`. Check the format of the file you saved.

## What does not work

- Vinted signs each photo address (`?s=`), so any edit returns 404. The largest public copy is `f800`, 800 px on the long side, although the page data lists 1200x1600 (2026-11-09).
- Squarespace sites never return more than 2500 px wide. For larger uploads, look in the site's asset library or on your own computer.
- Flickr `_o` originals use a different secret from the other sizes, so you cannot reach them by editing a thumbnail address.
- Unsplash+ photos on `plus.unsplash.com` carry an "Unsplash+" watermark on the larger copies (2026-11-13).
- Some Wayfair photos return a grey "No Image Available" card at every size above the page copy (2026-11-01).
- The old Tokopedia host `ecs7.tokopedia.net` returns 403 on the bare path.

The table is released under CC0 1.0.

I made PixLasso, a Chrome and Edge extension that applies these rules automatically when you save images: https://pixlasso.com/?src=github
