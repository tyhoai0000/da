<!doctype html>
	<html lang="en">

	<head>
		<meta charset="utf-8">
		<meta name="viewport" content="width=device-width, initial-scale=1">
		<title>Tiktok Printer</title>
		<meta name="description" content="Tiktok Printer Guess Words Game">
		<meta name="author" content="adierebel">
		<link rel="stylesheet" href="assets/css/reset.css?v=1.0">
		<link rel="stylesheet" href="assets/css/style.css?v=1.0">
		<link rel="stylesheet" href="https://www.w3schools.com/w3css/4/w3.css">
		<script type="text/javascript" src="words.js"></script>
		<script type="text/javascript" src="msg.js"></script>
		<script type="text/javascript" src="assets/tts/speakClient.js"></script>
		<script type="text/javascript" src="assets/js/jquery.js"></script>
		<script type="text/javascript" src="assets/js/socket.io.js"></script>
		<script type="text/javascript" src="assets/js/connection.js"></script>
		<script type="text/javascript" src="assets/js/app.js"></script>



	</head>

	<body
	background="https://images.rawpixel.com/image_800/cHJpdmF0ZS9sci9pbWFnZXMvd2Vic2l0ZS8yMDIyLTA1L3JtMjY3LW51bm55LTA0Yi5qcGc.jpg">

	<div class="w3-sidebar w3-bar-block w3-card w3-animate-left" style="display:none" id="mySidebar">
		<button style="background-color: lightblue;" class="w3-bar-item w3-button w3-large" onclick="w3_close()"> <center> <b> Close &times; </b></center> </button>
		<div class="info" style="margin-left: 10px;">
			<div class="text-bold">Live Chat</div>
			<div class="mb-3 mt-2">
				<input id="targetUsername" type="text" placeholder="Enter @username" style="width:140px;height:26px;vertical-align:middle;" />
				<button id="targetConnect" style="height:32px;vertical-align:middle;">✔ Connect</button>
			</div>
			<table class="mb-3" style="width:200px;">
				<tr>
					<td style="white-space:nowrap;">Canvas</td>
					<td>&nbsp;:&nbsp;</td>
					<td id="gameSize">&infin;</td>
				</tr>
				<tr>
					<td style="white-space:nowrap;">Chat Status</td>
					<td>&nbsp;:&nbsp;</td>
					<td id="stateText">Not Connected</td>
				</tr>
			</table>
			<div class="text-bold">Game:</div>
			<table class="mt-2 mb-2">
				<tr>
					<td>Next Word</td>
					<td>&nbsp;:&nbsp;</td>
					<td id="gameTimeout">&infin;</td>
				</tr>
				<tr>
					<td>Remain Words</td>
					<td>&nbsp;:&nbsp;</td>
					<td id="gameWords">&infin;</td>
				</tr>
			</table>
			<div class="mt-2 mb-3">
				<button id="btnGameToggle" style="height:32px;vertical-align:middle;">▶ MULAI</button>
				<button id="btnSkipWord" style="height:32px;vertical-align:middle;">➡ Lewati</button>
			</div>
			<div class="text-bold">Settings:</div>
			<table class="mt-2 mb-3">
				<tr>
					<td><input id="confComment" type="checkbox" checked="true" />&nbsp;&nbsp;</td>
					<td><label for="confComment">Cetak Komentar</label></td>
				</tr>
				<tr>
					<td><input id="confShare" type="checkbox" checked="true" />&nbsp;&nbsp;</td>
					<td><label for="confShare">Cetak Share &amp; Follow</label></td>
				</tr>
				<tr>
					<td><input id="confLike" type="checkbox" />&nbsp;&nbsp;</td>
					<td><label for="confLike">Cetak Like</label></td>
				</tr>
				<tr>
					<td><input id="confJoin" type="checkbox" />&nbsp;&nbsp;</td>
					<td><label for="confJoin">Cetak Pengguna Yang Bergabung</label></td>
				</tr>
				<tr>
					<td><input id="confBw" type="checkbox" />&nbsp;&nbsp;</td>
					<td><label for="confBw">Hitam &amp; Putih</label></td>
				</tr>
				<tr>
					<td><input id="confGlare" type="checkbox" />&nbsp;&nbsp;</td>
					<td><label for="confGlare">Aktifkan Warrna Overlay</label></td>
				</tr>
				<tr>
					<td><input id="confTTS" type="checkbox" checked="true" />&nbsp;&nbsp;</td>
					<td><label for="confTTS">Aktifkan Teks Menjadi Suara</label></td>
				</tr>
			</table>
			<div class="mb-3 mt-2">
				<div>Minimal Koin Untuk Mencetak Profil:</div>
				<input id="confMinGift" type="number" placeholder="Minimal Gift" value="1" min="1" style="width:100px;display:block;margin-top:2px;text-align:center" />
			</div>
			<div class="mb-3 mt-2">
				<div>UI Text:</div>
				<input id="confText0" type="text" style="width:200px;display:block;margin-top:2px;" value="" />
				<input id="confText1" type="text" style="width:200px;display:block;margin-top:2px;" value="" />
				<input id="confText2" type="text" style="width:200px;display:block;margin-top:2px;" value="" />
				<input id="confText3" type="text" style="width:200px;display:block;margin-top:2px;" value="" />
				<button id="btnSaveUI" class="mt-2">✔ Save</button>
			</div>
			<div class="mb-3 mt-3">
				<button id="btnResetSetting" class="mt-2">✖ Reset Pengaturan</button>
			</div>
			<div>
				<audio id="sfx1" class="d-block">
					<source src="assets/sounds/printer_comment.mp3" type="audio/mpeg">
					</audio>
					<audio id="sfx2" class="d-block">
						<source src="assets/sounds/printer_gift.mp3" type="audio/mpeg">
						</audio>
						<audio id="sfx3" class="d-block">
							<source src="assets/sounds/printer_winner.mp3" type="audio/mpeg">
							</audio>
							<audio id="sfx4" class="d-block">
								<source src="assets/sounds/yey.mp3" type="audio/mpeg">
								</audio>
								<audio id="tts" class="d-block"></audio>
							</div>
						</div>
					</div>

					<div id="main">
						<!-- <div class="w3-teal">
							<button id="openNav" class="w3-button w3-teal w3-xlarge" onclick="w3_open()">&#9776;</button>
						</div> -->
					</div>


					<div class="main">
						<div id="controlPanel" class="wrapper" onclick="w3_open()">
							<div class="container">
								<video class="background" autoplay muted loop>
									<source src="assets/media/background.mp4" type="video/mp4">
									</video>
									<div class="printer">
										<table class="table">
											<tr>
												<td id="paperContainer">
													<div id="paperPerspective" class="paperPerspective">
														<div id="paper" class="paper" style="font-size:12px;">
															<div style="width:100%;padding-top:100%;text-align:center;">
																<button id="btnPrepare" style="font-size:130%;">▶ Mulai Game</button>
															</div>
														</div>
													</div>
												</td>
											</tr>
											<tr class="bottom-container">
												<td class="bottom-wrapper">
													<div class="bottom-bar">
														<table id="textBottom" class="table" style="height:100%;font-size:16px;">
															<tr>
																<td
																style="vertical-align:middle;padding-left:7%;padding-right:3%;padding-top:5%;padding-bottom:1%;">
																<div id="textGuess" class="text-guess blink">
																	<div style='font-size:70%;padding-bottom:1.5%;'>***</div>
																	<div>***</div>
																</div>
															</td>
															<td
															style="width:40%;text-align:center;vertical-align:middle;padding-left:3%;padding-right:7%;padding-top:5%;padding-bottom:1%;font-size:80%;text-shadow: 2px 2px 5px #0000004f;">
															<div id="uiText0" style="font-size:80%;padding-bottom:3%;">Pemenang
															Terbaru 👑</div>
															<div style="padding-bottom:3%;">
																<img id="winnerAvatar" src="assets/media/profile.jpg" style="width:32px;height:32px;border-radius:50%;" />
															</div>
															<div id="textWinner" class="text-winner">***</div>
														</td>
													</tr>
													<tr>
														<td colspan="2" style="padding:1% 7%;vertical-align:middle;">
															<div class="text-caption" id="uiText1">🙋‍♀️🙋‍♂️ Tebak kata di atas
															</div>
														</td>
													</tr>
													<tr>
														<td colspan="2" style="padding:1% 7%;vertical-align:middle;">
															<div class="text-caption" id="uiText2">🎁 Kirim HADIAH untuk CETAK
															profil Anda</div>
														</td>
													</tr>

													<tr>
														<td colspan="2" style="padding:1% 7%;vertical-align:middle;">


														</td>
													</tr>



													<tr>
														<td colspan="2"
														style="padding:1% 7%;padding-bottom:7%;vertical-align:middle;">
														<div id="captionTTS" class="text-caption"
														style="margin-bottom: 0rem;">💬 Komen / katakan sesuatu untuk TTS
													</div>
												</td>
											</tr>
										</table>
									</div>
								</td>
							</tr>
						</table>
					</div>
					<div id="glareAnimation" class="animation" style="display:none;"></div>
				</div>
			</div>
		</div>
		<script>
			function w3_open() {
				document.getElementById("main").style.marginLeft = "75%";
				document.getElementById("mySidebar").style.width = "75%";
				document.getElementById("mySidebar").style.display = "block";
				document.getElementById("openNav").style.display = 'block';
			}
			function w3_close() {
				document.getElementById("main").style.marginLeft = "0%";
				document.getElementById("mySidebar").style.display = "none";
				document.getElementById("openNav").style.display = "inline-block";
			}
		</script>

	</body>

	</html>
