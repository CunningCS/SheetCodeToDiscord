# SheetCodeToDiscord
# Webhook from discord to push data from Google sheets 

function postToDiscord(cM,cSM,cTM) {
  const url = "DISCORD WEBHOOK"


  const message = {
      content: "@everyone\n<@&'Role.ID>\n<@"+cM+">\nGZW Name: " + cSM +"\nAs Of " + cTM 
    }


  const options = {
  'method' : 'post',
  'payload' : message
  };

  const res = UrlFetchApp.fetch(url,options)


}


function postFromSheet() {

  const ss = SpreadsheetApp.getActiveSpreadsheet()
  const ws = ss.getSheetByName("SHEETNAME")

  const mCdn = ws.getRange(ws.getMaxRows(),8).getNextDataCell(SpreadsheetApp.Direction.UP).offset(1,-4)
  const mSCgz = ws.getRange(ws.getMaxRows(),8).getNextDataCell(SpreadsheetApp.Direction.UP).offset(1,-5)
  const mTCqd = ws.getRange(ws.getMaxRows(),8).getNextDataCell(SpreadsheetApp.Direction.UP).offset(1,-2)

  const cM = mCdn.getValue()
  const cSM = mSCgz.getValue()
  const cTM = mTCqd.getValue()

  if(cM == "") return

  postToDiscord(cM, cSM, cTM)

  mCdn.offset(0,4).setValue("YES")

}
