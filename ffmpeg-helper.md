# 내 ffmpeg 명령어 모음 - 복붙용

**사용법**: `input.mp4`를 네 영상 파일명으로 바꾸고 파워쉘에 복붙

---

### 1. 용량 줄이기 - 화질 유지
ffmpeg -i input.mp4 -vcodec libx264 -crf 28 -preset fast output.mp4
`crf 28` 숫자 올리면 용량 더 작아짐. 23=고화질, 32=저화질

### 2. 유튜브 쇼츠용 세로 만들기 9:16
ffmpeg -i input.mp4 -vf "crop=ih*9/16:ih,scale=1080:1920" -c:a copy output_short.mp4
가운데 기준으로 잘림

### 3. 2배속 - 목소리 톤 유지
ffmpeg -i input.mp4 -filter:v "setpts=0.5*PTS" -filter:a "atempo=2.0" output_2x.mp4

### 4. 영상 자르기 - 10초부터 30초까지만
ffmpeg -ss 00:00:10 -to 00:00:30 -i input.mp4 -c copy output_cut.mp4

Code

### 5. 워터마크 넣기 - 오른쪽 아래
ffmpeg -i input.mp4 -i logo.png -filter_complex "overlay=W-w-10:H-h-10" -codec:a copy output_watermark.mp4
`logo.png` 파일이 영상과 같은 폴더에 있어야 함
