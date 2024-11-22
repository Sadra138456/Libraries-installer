<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Advanced Search Tool</title>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.3/css/all.min.css">
  <link rel="preconnect" href="https://fonts.gstatic.com">
  <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap" rel="stylesheet">
  <style>
    /* CSS Styles (unchanged) */
    body {
      font-family: 'Roboto', sans-serif;
      background-color: #1e1e1e;
      color: #ffffff;
      margin: 0;
      display: flex;
      height: 100vh;
    }

    .sidebar {
      width: 250px;
      background-color: #2a2a2a;
      padding: 20px;
      box-shadow: 2px 0 10px rgba(0, 0, 0, 0.5);
      position: relative;
      transition: width 0.3s;
    }

    .sidebar h3 {
      color: #007bff;
      margin-bottom: 20px;
    }

    .sidebar button {
      width: 100%;
      padding: 10px;
      background-color: #007bff;
      border: none;
      color: white;
      cursor: pointer;
      margin-bottom: 10px;
      border-radius: 5px;
      transition: background-color 0.3s;
    }

    .sidebar button:hover {
      background-color: #0056b3;
    }

    .content {
      flex-grow: 1;
      padding: 20px;
      background-color: #1e1e1e;
      position: relative;
    }

    .header {
      text-align: center;
      margin-bottom: 20px;
    }

    .title {
      font-size: 36px;
      font-weight: bold;
      margin-bottom: 20px;
      color: #007bff;
    }

    .beta-notice {
      font-size: 14px;
      color: #ffcc00;
      margin-bottom: 20px;
    }

    .search-bar {
      display: flex;
      justify-content: center;
      align-items: center;
      margin-bottom: 30px;
      position: relative;
    }

    .search-input {
      padding: 15px;
      font-size: 16px;
      border: 1px solid #007bff;
      border-radius: 30px;
      width: 400px;
      background-color: #2a2a2a;
      color: #ffffff;
      transition: border-color 0.3s;
      outline: none;
    }

    .search-input:focus {
      border-color: #0056b3;
    }

    .search-button, .voice-search {
      padding: 15px;
      background-color: #007bff;
      color: #fff;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      transition: background-color 0.3s;
      margin-left: 10px; /* Space between buttons */
    }

    .search-button:hover, .voice-search:hover {
      background-color: #0056b3;
    }

    .section-title {
      font-size: 24px;
      font-weight: bold;
      margin-bottom: 20px;
      color: #007bff;
    }

    .result-cards {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
      gap: 20px;
      list-style-type: none;
      padding: 0;
    }

    .result-cards .card {
      background-color: #2a2a2a;
      padding: 15px;
      border-radius: 8px;
      box-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
      transition: transform 0.3s, box-shadow 0.3s;
      position: relative;
      overflow: hidden;
    }

    .result-cards .card:hover {
      transform: translateY(-5px);
      box-shadow: 0 4px 20px rgba(0, 0, 0, 0.5);
    }

    .card-title {
      font-size: 20px;
      color: #007bff;
      margin: 0;
      transition: color 0.3s;
    }

    .card-title:hover {
      color: #0056b3;
    }

    .card-snippet {
      color: #cccccc;
      margin: 10px 0;
    }

    .card-image {
      width: 100%;
      height: 150px;
      object-fit: cover;
      border-radius: 8px;
      margin-bottom: 10px;
    }

    /* Fullscreen modal styles */
    .modal {
      display: none;
      position: fixed;
      z-index: 1000;
      left: 0;
      top: 0;
      width: 100%;
      height: 100%;
      background-color: rgba(0, 0, 0, 0.95);
      padding: 20px;
      overflow-y: auto;
    }

    .modal-content {
      background-color: #2a2a2a;
      border-radius: 8px;
      padding: 20px;
      color: #ffffff;
      max-height: 90%;
      overflow-y: auto;
      box-shadow: 0 0 20px rgba(0, 0, 0, 0.5);
    }

    .modal-title {
      font-size: 28px;
      margin-bottom: 10px;
      color: #007bff;
    }

    .close {
      color: #ffffff;
      float: right;
      font-size: 28px;
      font-weight: bold;
      cursor: pointer;
    }

    .modal-content p {
      line-height: 1.6; /* Improve readability */
      font-size: 18px; /* Increase font size for better visibility */
      margin: 10px 0; /* Add margin for spacing */
    }

    .footer {
      text-align: center;
      margin-top: 30px;
      color: #777;
    }

    /* Loading spinner */
    .loading {
      display: none;
      margin: 20px auto;
      border: 4px solid rgba(255, 255, 255, 0.3);
      border-top: 4px solid #007bff;
      border-radius: 50%;
      width: 40px;
      height: 40px;
      animation: spin 1s linear infinite;
    }

    @keyframes spin {
      0% { transform: rotate(0deg); }
      100% { transform: rotate(360deg); }
    }

    /* Media Queries for responsiveness */
    @media (max-width: 768px) {
      .sidebar {
        width: 200px;
      }

      .search-input {
        width: 100%;
      }

      .title {
        font-size: 28px;
      }

      .section-title {
        font-size: 20px;
      }
    }

    @media (max-width: 576px) {
      .sidebar {
        width: 100%;
        position: absolute;
        height: auto;
        z-index: 100;
      }

      .content {
        padding: 10px;
      }

      .search-input {
        width: calc(100% - 40px);
      }

      .search-button {
        width: 40px;
      }
    }
  </style>
</head>
<body>
  <div class="sidebar">
    <h3>Topics</h3>
    <button onclick="setTopic('wiki')">Wikipedia</button>
    <button onclick="setTopic('programming')">Programming</button>
    <button onclick="setTopic('travel')">Travel</button>
    <button onclick="setTopic('movies')">Movies</button>
  </div>

  <div class="content">
    <header class="header">
      <h1 class="title">Advanced Search Tool</h1>
      <div class="beta-notice">This is a beta version and is under improvement.</div>
      <div class="search-bar">
        <input type="text" class="search-input" placeholder="Search..." />
        <button class="search-button" onclick="performSearch()">
          <i class="fas fa-search"></i>
        </button>
        <button class="voice-search" onclick="startVoiceSearch()">
          <i class="fas fa-microphone"></i>
        </button>
      </div>
      <div class="loading" id="loading"></div>
    </header>

    <div class="search-results">
      <h2 class="section-title">Search Results</h2>
      <div class="result-cards"></div>
    </div>
  </div>

  <!-- Fullscreen modal for displaying article content -->
  <div id="myModal" class="modal">
    <div class="modal-content">
      <span class="close" onclick="closeModal()">&times;</span>
      <h2 class="modal-title" id="modal-title"></h2>
      <div id="modal-content" style="white-space: pre-wrap;"></div>
    </div>
  </div>

  <script>
    const searchInput = document.querySelector('.search-input');
    const resultCards = document.querySelector('.result-cards');
    const modal = document.getElementById('myModal');
    const modalTitle = document.getElementById('modal-title');
    const modalContent = document.getElementById('modal-content');
    const loadingSpinner = document.getElementById('loading');
    let currentTopic = 'wiki'; // Default topic

    function setTopic(topic) {
      currentTopic = topic;
      searchInput.placeholder = `Search in ${topic === 'wiki' ? 'Wikipedia' : topic}`;
      resultCards.innerHTML = ''; // Clear previous results
    }

    function performSearch() {
      const query = searchInput.value.trim();
      if (query) {
        loadingSpinner.style.display = 'block'; // Show loading spinner
        if (currentTopic === 'wiki') {
          fetchWikipediaResults(query)
            .then(results => {
              displaySearchResults(results);
            })
            .catch(error => {
              console.error('Error fetching Wikipedia results:', error);
              alert('Error loading results. Please try again.');
            })
            .finally(() => {
              loadingSpinner.style.display = 'none'; // Hide loading spinner
            });
        } else if (currentTopic === 'programming') {
          // Implement programming search logic here
          alert('Programming search functionality is not yet implemented.');
        } else if (currentTopic === 'travel') {
          // Implement travel search logic here
          alert('Travel search functionality is not yet implemented.');
        } else if (currentTopic === 'movies') {
          fetchMovieResults(query)
            .then(results => {
              displayMovieResults(results);
            })
            .catch(error => {
              console.error('Error fetching movie results:', error);
              alert('Error loading movie results. Please try again.');
            })
            .finally(() => {
              loadingSpinner.style.display = 'none'; // Hide loading spinner
            });
        }
      }
    }

    function fetchWikipediaResults(query) {
      return fetch(`https://en.wikipedia.org/w/api.php?action=query&list=search&srsearch=${query}&format=json&origin=*`)
        .then(response => {
          if (!response.ok) {
            throw new Error('Network response was not ok');
          }
          return response.json();
        })
        .then(data => data.query.search);
    }

    function fetchMovieResults(query) {
      const apiKey = 'YOUR_OMDB_API_KEY'; // Replace with your OMDb API key
      return fetch(`https://www.omdbapi.com/?s=${query}&apikey=${apiKey}`)
        .then(response => {
          if (!response.ok) {
            throw new Error('Network response was not ok');
          }
          return response.json();
        })
        .then(data => data.Search || []);
    }

    function displaySearchResults(results) {
      resultCards.innerHTML = '';
      if (results.length === 0) {
        resultCards.innerHTML = '<p>No results found.</p>';
        return;
      }
      results.forEach(result => {
        const card = document.createElement('div');
        card.classList.add('card');
        card.innerHTML = `
          <img src="https://via.placeholder.com/300x150" alt="${result.title}" class="card-image" />
          <h3 class="card-title" onclick="fetchArticleContent('${result.title}')">${result.title}</h3>
          <p class="card-snippet">${result.snippet}</p>
        `;
        resultCards.appendChild(card);
      });
    }

    function displayMovieResults(results) {
      resultCards.innerHTML = '';
      if (results.length === 0) {
        resultCards.innerHTML = '<p>No results found.</p>';
        return;
      }
      results.forEach(result => {
        const card = document.createElement('div');
        card.classList.add('card');
        card.innerHTML = `
          <img src="${result.Poster !== "N/A" ? result.Poster : 'https://via.placeholder.com/300x150'}" alt="${result.Title}" class="card-image" />
          <h3 class="card-title">${result.Title}</h3>
          <p class="card-snippet">Year: ${result.Year}</p>
        `;
        resultCards.appendChild(card);
      });
    }

    function fetchArticleContent(title) {
      loadingSpinner.style.display = 'block'; // Show loading spinner
      fetch(`https://en.wikipedia.org/w/api.php?action=query&prop=extracts&explaintext=&titles=${title}&format=json&origin=*`)
        .then(response => {
          if (!response.ok) {
            throw new Error('Network response was not ok');
          }
          return response.json();
        })
        .then(data => {
          const page = Object.values(data.query.pages)[0];
          modalTitle.innerText = page.title;
          modalContent.innerText = page.extract || 'No content available.';
          modal.style.display = 'block'; // Show modal
        })
        .catch(error => {
          console.error('Error fetching article content:', error);
          alert('Error loading article content. Please try again.');
        })
        .finally(() => {
          loadingSpinner.style.display = 'none'; // Hide loading spinner
        });
    }

    function closeModal() {
      modal.style.display = 'none';
    }

    function startVoiceSearch() {
      const recognition = new (window.SpeechRecognition || window.webkitSpeechRecognition)();
      recognition.lang = 'en-US';
      recognition.start();

      recognition.onresult = function(event) {
        const transcript = event.results[0][0].transcript;
        searchInput.value = transcript;
        performSearch();
      };

      recognition.onerror = function(event) {
        console.error('Error in voice search:', event.error);
      };
    }
  </script>
</body>
</html>
