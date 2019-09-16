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
