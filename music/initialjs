const image = document.querySelector('img')
const title = document.getElementById("title")
const artist = document.getElementById("artist")

const music = document.querySelector("audio");
const prevBtn = document.getElementById("prev")
const playBtn = document.getElementById("play")
const nextBtn = document.getElementById("next")
const progressContainer = document.getElementById("progress-container")
const progress = document.getElementById("progress")
const durationEl = document.getElementById("duration")
const currentEl = document.getElementById("current-time")


const songs = [
    {
        name:'jacinto-1',
        displayName:'Electric Chill Machine',
        artist:"Jacinto Design"
    },
    {
        name:'jacinto-2',
        displayName:'Seven Nation Army',
        artist:"Jacinto Design"
    },
    {
        name:'jacinto-3',
        displayName:'Electric Chill Machine',
        artist:"Jacinto Design"
    },
    {
        name:'metric-1',
        displayName:'Front Row',
        artist:"Metric/Jacinto Design"
    }
]

//Song index
let songIndex = 0

//Check if playing 
let isPlaying= false;


//Play 
const playSong = () => {
    isPlaying = true
    playBtn.classList.replace('fa-play', 'fa-pause')
    playBtn.setAttribute('title','Pause')
    music.play()
}

//pause 
const pauseSong = () => {
    isPlaying = false
    playBtn.classList.replace('fa-pause', 'fa-play')
    playBtn.setAttribute('title','Play')
    music.pause()
}

const loadSong = (song) => {
    title.textContent = song.displayName
    artist.textContent = song.artist
    music.src = `music/${song.name}.mp3`
    image.src = `img/${song.name}.jpg`
}

//onLoad - select first song
loadSong(songs[songIndex])


const prevSong = () => {
    songIndex--
    if (songIndex < 0)
        songIndex = songs.length-1
    loadSong(songs[songIndex])
    playSong()
}

const nextSong = () => {
    songIndex++
    if (songIndex === songs.length)
        songIndex = 0
    loadSong(songs[songIndex])
    playSong()
}

//Play/Pause Prev and nextBtn functionality
playBtn.addEventListener('click', () => isPlaying? pauseSong() : playSong())
prevBtn.addEventListener('click', prevSong)
nextBtn.addEventListener('click', nextSong)


const updateProgressbar = e => {
    if (isPlaying){
        const {currentTime, duration} = e.srcElement 
        const progressing = (currentTime/duration) * 100
        progress.style.width = `${progressing}%`

        //Calculate duration 
        let durationMinutes = Math.floor(duration/60)
        let durationSeconds = Math.floor(duration%60)
        if (durationSeconds < 10)
            durationSeconds = `0${durationSeconds}`
        
        //Delay switching duration to avoid NaN
        if (durationSeconds)
        durationEl.textContent = `${durationMinutes}:${durationSeconds}`

        //Calculate current time 
        let currentMinutes = Math.floor(currentTime/60)
        let currentSeconds = Math.floor(currentTime%60)
        if (currentSeconds < 10)
            currentSeconds = `0${currentSeconds}`
            currentEl.textContent = `${currentMinutes}:${currentSeconds}`
    }
}

const setProgressBar = e => {
    const {clientWidth} = e.srcElement
    const clickX = e.offsetX
    const {duration} =  music
    music.currentTime = (clickX/clientWidth)*duration   
}


//Progress container/Progress functionality
music.addEventListener('timeupdate',updateProgressbar)
music.addEventListener('ended',nextSong)
progressContainer.addEventListener('click', setProgressBar)