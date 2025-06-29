---
layout: default
title: NKS API
description: API documentation for nks-api
theme: jekyll-theme-hacker
---

# NKS API

Welcome to the NKS API documentation. This site provides information about the API endpoints and how to use them.

## Overview

The NKS API provides race prediction data for horse racing events. You can access race data by specifying a race ID.

## Getting Started

To use the API, simply make a GET request to the endpoint with the race ID.

## API Endpoints

### Race Data

Endpoint: `/api/v1/{race_id}.json`

Example: `/api/v1/202508020503.json`

## Try It Out

<div class="try-it-out">
  <form id="race-form">
    <label for="race-id">Enter Race ID:</label>
    <input type="text" id="race-id" name="race-id" placeholder="e.g., 202508020503" required>
    <button type="submit">Get Race Data</button>
  </form>

  <div id="result-container" style="display: none;">
    <h3>Result:</h3>
    <pre id="json-result" style="background-color: rgba(0,0,0,0.9); padding: 10px; overflow: auto; max-height: 500px;"></pre>
  </div>

  <div id="error-container" style="display: none; color: red;"></div>
</div>

<script>
document.getElementById('race-form').addEventListener('submit', function(event) {
  event.preventDefault();

  const raceId = document.getElementById('race-id').value.trim();
  const resultContainer = document.getElementById('result-container');
  const jsonResult = document.getElementById('json-result');
  const errorContainer = document.getElementById('error-container');

  // Reset display
  resultContainer.style.display = 'none';
  errorContainer.style.display = 'none';

  // Validate race ID format (assuming it should be a number)
  if (!raceId.match(/^\d+$/)) {
    errorContainer.textContent = 'Invalid race ID format. Please enter a numeric ID.';
    errorContainer.style.display = 'block';
    return;
  }

  // Fetch the race data
  fetch(`https://shahoxo.github.io/nks-api/api/v1/${raceId}.json`)
    .then(response => {
      if (!response.ok) {
        throw new Error(`HTTP error! Status: ${response.status}`);
      }
      return response.json();
    })
    .then(data => {
      // Display the JSON data
      jsonResult.textContent = JSON.stringify(data, null, 2);
      resultContainer.style.display = 'block';
    })
    .catch(error => {
      errorContainer.textContent = `Error: ${error.message}`;
      errorContainer.style.display = 'block';
    });
});
</script>
