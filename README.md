# Beat-closet-
beat-closet/
├─ index.html
├─ beats/
│   ├─ chill_vibes.mp3
│   ├─ trap_heat.mp3
│   └─ ...
├─ images/
004ad97c2c341a8ea348c244089447a7.jpg
85239b9b1cedb71ea6ac8b190e3b03a7.jpg
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Beat Closet</title>
<style>
body {margin:0;font-family:'Arial',sans-serif;background:#0d0d0d;color:#fff;}
header {text-align:center;padding:40px 0;font-size:3em;font-weight:bold;background:linear-gradient(90deg,#ff4d6d,#6b5bff);letter-spacing:2px;box-shadow:0 4px 20px rgba(0,0,0,0.5);}
#search {display:block;margin:20px auto;width:80%;padding:12px;border-radius:25px;border:none;background:#1a1a1a;color:#fff;font-size:1em;}
.beat-container {display:grid;grid-template-columns:repeat(auto-fit,minmax(250px,1fr));gap:25px;padding:20px;}
.beat-card {position:relative;border-radius:15px;overflow:hidden;cursor:pointer;background:rgba(255,255,255,0.05);backdrop-filter:blur(10px);transition:transform 0.3s,box-shadow 0.3s;}
.beat-card:hover {transform:translateY(-5px);box-shadow:0 10px 25px rgba(255,77,109,0.4);}
.beat-card img {width:100%;height:200px;object-fit:cover;display:block;}
.overlay {position:absolute;top:0;left:0;width:100%;height:100%;background:rgba(0,0,0,0.5);opacity:0;transition:opacity 0.3s;display:flex;justify-content:center;align-items:center;}
.beat-card:hover .overlay {opacity:1;}
.play-btn {background:#ff4d6d;border:none;padding:15px 25px;border-radius:50px;font-size:1.2em;color:#fff;cursor:pointer;transition:transform 0.2s;}
.play-btn:hover {transform:scale(1.2);}
.beat-info {padding:15px;text-align:center;}
.beat-info h3 {margin:10px 0 5px;}
.beat-info p {margin:0;font-size:0.9em;color:#aaa;}
audio {width:90%;margin:10px auto;display:block;}
</style>
</head>
<body>

<header>My Beat Closet</header>
<input type="text" id="search" placeholder="Search beats by name or genre...">
<div class="beat-container" id="beatContainer"></div>

<script>
// === ADD YOUR BEATS HERE ===
const beats = [
  {
    title: "Chill Vibes",
    genre: "Lofi",
    img: "images/chill_vibes.jpg",
    audio: "beats/chill_vibes.mp3"
  },
  {
    title: "Trap Heat",
    genre: "Trap",
    img: "images/trap_heat.jpg",
    audio: "beats/trap_heat.mp3"
  }
  // Add more beats here
];

const beatContainer = document.getElementById('beatContainer');

function renderBeats(){
  beatContainer.innerHTML='';
  beats.forEach(beat=>{
    const card=document.createElement('div');
    card.classList.add('beat-card');
    card.dataset.title=beat.title;
    card.dataset.genre=beat.genre;
    card.innerHTML=`
      <img src="${beat.img}" alt="${beat.title}">
      <div class="overlay">
        <button class="play-btn">▶ Play</button>
      </div>
      <div class="beat-info">
        <h3>${beat.title}</h3>
        <p>Genre: ${beat.genre}</p>
        <audio src="${beat.audio}"></audio>
      </div>
    `;
    beatContainer.appendChild(card);
  });

  // Play button functionality
  document.querySelectorAll('.play-btn').forEach(btn=>{
    btn.addEventListener('click', e=>{
      e.stopPropagation();
      const audio=btn.closest('.beat-card').querySelector('audio');
      if(audio.paused){
        document.querySelectorAll('audio').forEach(a=>a.pause());
        audio.play();
      }else audio.pause();
    });
  });
}

renderBeats();

// === SEARCH FUNCTIONALITY ===
document.getElementById('search').addEventListener('input', e=>{
  const query=e.target.value.toLowerCase();
  document.querySelectorAll('.beat-card').forEach(card=>{
    const title=card.dataset.title.toLowerCase();
    const genre=card.dataset.genre.toLowerCase();
    card.style.display=(title.includes(query)||genre.includes(query))?'block':'none';
  });
});
</script>

</body>
</html>
