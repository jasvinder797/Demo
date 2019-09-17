 var express = require('express'),
 router = express.Router();

router.use("/user", require("../controllers/user.api"));
router.use("/grade", require("../controllers/grade.api"));
router.use("/fee", require("../controllers/fee.api"));
router.use("/contact", require("../controllers/contact.api"));
router.use("/profile", require("../controllers/profile.api"));
//router.use("/notification", require("../controllers/notification.api"));
router.use("/attendance", require("../controllers/attendance.api"));
router.use("/dimages", require("../controllers/dimages.api"));
 
module.exports = router;



app.use(session({
  name: 'sid',
  secret: 'sdkfskdfkds',
  resave: false,
  saveUninitialized: false,
  cookie: { secure: false, sameSite: true, maxAge: 50000 },
  
}))



const adminCheck = (req,res,next) =>{
  if(req.session.userId==1){
    console.log('you are done')
    next()
  }
  else{
    console.log("byee byee")
  }
}



#
const express = require('express');
const jwt = require('jsonwebtoken');

const app = express();

app.get('/api', (req, res) => {
  res.json({
    message: 'Welcome to the API'
  });
});

app.post('/api/posts', verifyToken, (req, res) => {  
  jwt.verify(req.token, 'secretkey', (err, authData) => {
    if(err) {
      res.sendStatus(403);
    } else {
      res.json({
        message: 'Post created...',
        authData
      });
    }
  });
});

app.post('/api/login', (req, res) => {
  // Mock user
  const user = {
    id: 1, 
    username: 'brad',
    email: 'brad@gmail.com'
  }

  jwt.sign({user}, 'secretkey', { expiresIn: '30s' }, (err, token) => {
    res.json({
      token
    });
  });
});

// FORMAT OF TOKEN
// Authorization: Bearer <access_token>

// Verify Token
function verifyToken(req, res, next) {
  // Get auth header value
  const bearerHeader = req.headers['authorization'];
  // Check if bearer is undefined
  if(typeof bearerHeader !== 'undefined') {
    // Split at the space
    const bearer = bearerHeader.split(' ');
    // Get token from array
    const bearerToken = bearer[1];
    // Set the token
    req.token = bearerToken;
    // Next middleware
    next();
  } else {
    // Forbidden
    res.sendStatus(403);
  }

}

app.listen(5000, () => console.log('Server started on port 5000'));
