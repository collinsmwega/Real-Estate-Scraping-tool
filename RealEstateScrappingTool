function scrapeRealEstateDataHybridApproach() {
  // URL of the real estate site you want to scrape

  var url = 'URL';//Replace with the actual URL

  // Fetch the webpage content
  var response = UrlFetchApp.fetch(url);

  //Parse the HTML content
  var htmlContent = response.getContentText();
  var parsedHtml = HtmlService.createHtmlOutput(htmlContent).getContent();

  //Example: Extracting property names (assuming they are within span tag)
  var descriptionRegex = /<span class="p24_content">(.*?)<\/span>/g;
  var descriptionMatches = htmlContent.match(descriptionRegex) || [];

  // check if no matches found based on the provided class name
  if(descriptionMatches.length === 0){
    Logger.log("No matches found based on the provided class name.");
    return;
  }

  // combine the matches
  var combinedMatches = [];
  for (var i = 0; i < descriptionMatches.length; i++){
    combinedMatches.push([descriptionMatches[i]]);
  }

  //Prepare data for google sheet
  var data = combinedMatches.map(function(match){
    return [match[0].replace(/<span class="p24_content">|<\/span>/g, '').trim()];
  });

  // check if there is no data to write to the sheet
  if(data.length ===0 ){
    logger.log("No data to write to the sheet.");
    return;
  }

  // write data to google sheet
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();

    sheet.getRange(1,1, data.length, 2).setValues(data);
}
