/*
@license
dhtmlxScheduler v.5.1.6 Stardard

This software is covered by GPL license. You also can obtain Commercial or Enterprise license to use it in non-GPL project - please contact sales@dhtmlx.com. Usage without proper license is prohibited.

(c) Dinamenta, UAB.
*/

'use strict';
/**
 * @param {string} funcObject
 * @param {string} dhtmlObject
 * @param {!Object} async
 * @param {string} rSeed
 * @return {?}
 */
function dtmlXMLLoaderObject(funcObject, dhtmlObject, async, rSeed) {
  return this.xmlDoc = "", "undefined" != typeof async ? this.async = async : this.async = true, this.onloadAction = funcObject || null, this.mainObject = dhtmlObject || null, this.waitCall = null, this.rSeed = rSeed || false, this;
}
/**
 * @param {string} s
 * @return {?}
 */
function convertStringToBoolean(s) {
  switch("string" == typeof s && (s = s.toLowerCase()), s) {
    case "1":
    case "true":
    case "yes":
    case "y":
    case 1:
    case true:
      return true;
    default:
      return false;
  }
}
/**
 * @param {string} str
 * @return {?}
 */
function getUrlSymbol(str) {
  return -1 != str.indexOf("?") ? "&" : "?";
}
/**
 * @return {?}
 */
function dhtmlDragAndDropObject() {
  return window.dhtmlDragAndDrop ? window.dhtmlDragAndDrop : (this.lastLanding = 0, this.dragNode = 0, this.dragStartNode = 0, this.dragStartObject = 0, this.tempDOMU = null, this.tempDOMM = null, this.waitDrag = 0, window.dhtmlDragAndDrop = this, this);
}
/**
 * @param {?} type
 * @param {?} name
 * @param {?} params
 * @return {?}
 */
function _dhtmlxError(type, name, params) {
  return this.catches || (this.catches = []), this;
}
/**
 * @param {!Object} a
 * @param {!Object} b
 * @return {?}
 */
function dhtmlXHeir(a, b) {
  var prop;
  for (prop in b) {
    if ("function" == typeof b[prop]) {
      a[prop] = b[prop];
    }
  }
  return a;
}
window.dhtmlXScheduler = window.scheduler = {
  version : "5.1.6"
}, window.dhtmlx || (dhtmlx = function(obj) {
  var a;
  for (a in obj) {
    dhtmlx[a] = obj[a];
  }
  return dhtmlx;
}), dhtmlx.extend_api = function(name, map, ext) {
  var fn = window[name];
  if (fn) {
    /**
     * @param {!Object} obj
     * @return {?}
     */
    window[name] = function(obj) {
      var _ref12;
      if (obj && "object" == typeof obj && !obj.tagName) {
        _ref12 = fn.apply(this, map._init ? map._init(obj) : arguments);
        var a;
        for (a in dhtmlx) {
          if (map[a]) {
            this[map[a]](dhtmlx[a]);
          }
        }
        for (a in obj) {
          if (map[a]) {
            this[map[a]](obj[a]);
          } else {
            if (0 === a.indexOf("on")) {
              this.attachEvent(a, obj[a]);
            }
          }
        }
      } else {
        _ref12 = fn.apply(this, arguments);
      }
      return map._patch && map._patch(this), _ref12 || this;
    };
    window[name].prototype = fn.prototype;
    if (ext) {
      dhtmlXHeir(window[name].prototype, ext);
    }
  }
}, dhtmlxAjax = {
  get : function(url, callback) {
    var t = new dtmlXMLLoaderObject(true);
    return t.async = arguments.length < 3, t.waitCall = callback, t.loadXML(url), t;
  },
  post : function(url, post, callback) {
    var t = new dtmlXMLLoaderObject(true);
    return t.async = arguments.length < 4, t.waitCall = callback, t.loadXML(url, true, post), t;
  },
  getSync : function(obj) {
    return this.get(obj, null, true);
  },
  postSync : function(data, type) {
    return this.post(data, type, null, true);
  }
}, window.dtmlXMLLoaderObject = dtmlXMLLoaderObject, dtmlXMLLoaderObject.count = 0, dtmlXMLLoaderObject.prototype.waitLoadFunction = function(dhtmlObject) {
  /** @type {boolean} */
  var t = true;
  return this.check = function() {
    if (dhtmlObject && dhtmlObject.onloadAction && (!dhtmlObject.xmlDoc.readyState || 4 == dhtmlObject.xmlDoc.readyState)) {
      if (!t) {
        return;
      }
      /** @type {boolean} */
      t = false;
      dtmlXMLLoaderObject.count++;
      if ("function" == typeof dhtmlObject.onloadAction) {
        dhtmlObject.onloadAction(dhtmlObject.mainObject, null, null, null, dhtmlObject);
      }
      if (dhtmlObject.waitCall) {
        dhtmlObject.waitCall.call(this, dhtmlObject);
        /** @type {null} */
        dhtmlObject.waitCall = null;
      }
    }
  }, this.check;
}, dtmlXMLLoaderObject.prototype.getXMLTopNode = function(tagName, oldObj) {
  var z;
  if (this.xmlDoc.responseXML) {
    var children = this.xmlDoc.responseXML.getElementsByTagName(tagName);
    if (0 === children.length && -1 != tagName.indexOf(":")) {
      children = this.xmlDoc.responseXML.getElementsByTagName(tagName.split(":")[1]);
    }
    z = children[0];
  } else {
    z = this.xmlDoc.documentElement;
  }
  if (z) {
    return this._retry = false, z;
  }
  if (!this._retry && _isIE) {
    /** @type {boolean} */
    this._retry = true;
    oldObj = this.xmlDoc;
    return this.loadXMLString(this.xmlDoc.responseText.replace(/^[\s]+/, ""), true), this.getXMLTopNode(tagName, oldObj);
  }
  return dhtmlxError.throwError("LoadXML", "Incorrect XML", [oldObj || this.xmlDoc, this.mainObject]), document.createElement("div");
}, dtmlXMLLoaderObject.prototype.loadXMLString = function(txt, caseSensitive) {
  if (_isIE) {
    this.xmlDoc = new ActiveXObject("Microsoft.XMLDOM");
    this.xmlDoc.async = this.async;
    /**
     * @return {undefined}
     */
    this.xmlDoc.onreadystatechange = function() {
    };
    this.xmlDoc.loadXML(txt);
  } else {
    /** @type {!DOMParser} */
    var parser = new DOMParser;
    /** @type {(Document|null)} */
    this.xmlDoc = parser.parseFromString(txt, "text/xml");
  }
  if (!caseSensitive) {
    if (this.onloadAction) {
      this.onloadAction(this.mainObject, null, null, null, this);
    }
    if (this.waitCall) {
      this.waitCall();
      /** @type {null} */
      this.waitCall = null;
    }
  }
}, dtmlXMLLoaderObject.prototype.loadXML = function(path, data, value, options) {
  if (this.rSeed) {
    /** @type {string} */
    path = path + ((-1 != path.indexOf("?") ? "&" : "?") + "a_dhx_rSeed=" + (new Date).valueOf());
  }
  /** @type {string} */
  this.filePath = path;
  if (!_isIE && window.XMLHttpRequest) {
    /** @type {!XMLHttpRequest} */
    this.xmlDoc = new XMLHttpRequest;
  } else {
    this.xmlDoc = new ActiveXObject("Microsoft.XMLHTTP");
  }
  if (this.async) {
    this.xmlDoc.onreadystatechange = new this.waitLoadFunction(this);
  }
  if ("string" == typeof data) {
    this.xmlDoc.open(data, path, this.async);
  } else {
    this.xmlDoc.open(data ? "POST" : "GET", path, this.async);
  }
  if (options) {
    this.xmlDoc.setRequestHeader("User-Agent", "dhtmlxRPC v0.1 (" + navigator.userAgent + ")");
    this.xmlDoc.setRequestHeader("Content-type", "text/xml");
  } else {
    if (data) {
      this.xmlDoc.setRequestHeader("Content-type", "application/x-www-form-urlencoded");
    }
  }
  this.xmlDoc.setRequestHeader("X-Requested-With", "XMLHttpRequest");
  this.xmlDoc.send(value);
  if (!this.async) {
    (new this.waitLoadFunction(this))();
  }
}, dtmlXMLLoaderObject.prototype.destructor = function() {
  return this._filterXPath = null, this._getAllNamedChilds = null, this._retry = null, this.async = null, this.rSeed = null, this.filePath = null, this.onloadAction = null, this.mainObject = null, this.xmlDoc = null, this.doXPath = null, this.doXPathOpera = null, this.doXSLTransToObject = null, this.doXSLTransToString = null, this.loadXML = null, this.loadXMLString = null, this.doSerialization = null, this.xmlNodeToJSON = null, this.getXMLTopNode = null, this.setXSLParamValue = null, null;
}, dtmlXMLLoaderObject.prototype.xmlNodeToJSON = function(node) {
  var t = {};
  /** @type {number} */
  var i = 0;
  for (; i < node.attributes.length; i++) {
    t[node.attributes[i].name] = node.attributes[i].value;
  }
  t._tagvalue = node.firstChild ? node.firstChild.nodeValue : "";
  /** @type {number} */
  i = 0;
  for (; i < node.childNodes.length; i++) {
    var nodeName = node.childNodes[i].tagName;
    if (nodeName) {
      if (!t[nodeName]) {
        /** @type {!Array} */
        t[nodeName] = [];
      }
      t[nodeName].push(this.xmlNodeToJSON(node.childNodes[i]));
    }
  }
  return t;
}, window.dhtmlDragAndDropObject = dhtmlDragAndDropObject, dhtmlDragAndDropObject.prototype.removeDraggableItem = function(htmlNode) {
  /** @type {null} */
  htmlNode.onmousedown = null;
  /** @type {null} */
  htmlNode.dragStarter = null;
  /** @type {null} */
  htmlNode.dragLanding = null;
}, dhtmlDragAndDropObject.prototype.addDraggableItem = function(htmlNode, dhtmlObject) {
  htmlNode.onmousedown = this.preCreateDragCopy;
  /** @type {string} */
  htmlNode.dragStarter = dhtmlObject;
  this.addDragLanding(htmlNode, dhtmlObject);
}, dhtmlDragAndDropObject.prototype.addDragLanding = function(htmlNode, dhtmlObject) {
  /** @type {!Object} */
  htmlNode.dragLanding = dhtmlObject;
}, dhtmlDragAndDropObject.prototype.preCreateDragCopy = function(e) {
  return !e && !window.event || 2 != (e || event).button ? window.dhtmlDragAndDrop.waitDrag ? (window.dhtmlDragAndDrop.waitDrag = 0, document.body.onmouseup = window.dhtmlDragAndDrop.tempDOMU, document.body.onmousemove = window.dhtmlDragAndDrop.tempDOMM, false) : (window.dhtmlDragAndDrop.dragNode && window.dhtmlDragAndDrop.stopDrag(e), window.dhtmlDragAndDrop.waitDrag = 1, window.dhtmlDragAndDrop.tempDOMU = document.body.onmouseup, window.dhtmlDragAndDrop.tempDOMM = document.body.onmousemove, window.dhtmlDragAndDrop.dragStartNode = 
  this, window.dhtmlDragAndDrop.dragStartObject = this.dragStarter, document.body.onmouseup = window.dhtmlDragAndDrop.preCreateDragCopy, document.body.onmousemove = window.dhtmlDragAndDrop.callDrag, window.dhtmlDragAndDrop.downtime = (new Date).valueOf(), e && e.preventDefault ? (e.preventDefault(), false) : false) : void 0;
}, dhtmlDragAndDropObject.prototype.callDrag = function(e) {
  if (!e) {
    e = window.event;
  }
  var self = window.dhtmlDragAndDrop;
  if (!((new Date).valueOf() - self.downtime < 100)) {
    if (!self.dragNode) {
      if (!self.waitDrag) {
        return self.stopDrag(e, true);
      }
      if (self.dragNode = self.dragStartObject._createDragNode(self.dragStartNode, e), !self.dragNode) {
        return self.stopDrag();
      }
      /**
       * @return {?}
       */
      self.dragNode.onselectstart = function() {
        return false;
      };
      self.gldragNode = self.dragNode;
      document.body.appendChild(self.dragNode);
      document.body.onmouseup = self.stopDrag;
      /** @type {number} */
      self.waitDrag = 0;
      /** @type {!Window} */
      self.dragNode.pWindow = window;
      self.initFrameRoute();
    }
    if (self.dragNode.parentNode != window.document.body && self.gldragNode) {
      var grd = self.gldragNode;
      if (self.gldragNode.old) {
        grd = self.gldragNode.old;
      }
      grd.parentNode.removeChild(grd);
      var oldBody = self.dragNode.pWindow;
      if (grd.pWindow && grd.pWindow.dhtmlDragAndDrop.lastLanding && grd.pWindow.dhtmlDragAndDrop.lastLanding.dragLanding._dragOut(grd.pWindow.dhtmlDragAndDrop.lastLanding), _isIE) {
        /** @type {!Element} */
        var div = document.createElement("div");
        div.innerHTML = self.dragNode.outerHTML;
        /** @type {!Node} */
        self.dragNode = div.childNodes[0];
      } else {
        self.dragNode = self.dragNode.cloneNode(true);
      }
      /** @type {!Window} */
      self.dragNode.pWindow = window;
      self.gldragNode.old = self.dragNode;
      document.body.appendChild(self.dragNode);
      oldBody.dhtmlDragAndDrop.dragNode = self.dragNode;
    }
    /** @type {string} */
    self.dragNode.style.left = e.clientX + 15 + (self.fx ? -1 * self.fx : 0) + (document.body.scrollLeft || document.documentElement.scrollLeft) + "px";
    /** @type {string} */
    self.dragNode.style.top = e.clientY + 3 + (self.fy ? -1 * self.fy : 0) + (document.body.scrollTop || document.documentElement.scrollTop) + "px";
    var z;
    z = e.srcElement ? e.srcElement : e.target;
    self.checkLanding(z, e);
  }
}, dhtmlDragAndDropObject.prototype.calculateFramePosition = function(n) {
  if (window.name) {
    var el = parent.frames[window.name].frameElement.offsetParent;
    /** @type {number} */
    var fx = 0;
    /** @type {number} */
    var fy = 0;
    for (; el;) {
      fx = fx + el.offsetLeft;
      fy = fy + el.offsetTop;
      el = el.offsetParent;
    }
    if (parent.dhtmlDragAndDrop) {
      var currentDataItemIdentifyingStr = parent.dhtmlDragAndDrop.calculateFramePosition(1);
      fx = fx + 1 * currentDataItemIdentifyingStr.split("_")[0];
      fy = fy + 1 * currentDataItemIdentifyingStr.split("_")[1];
    }
    if (n) {
      return fx + "_" + fy;
    }
    this.fx = fx;
    this.fy = fy;
  }
  return "0_0";
}, dhtmlDragAndDropObject.prototype.checkLanding = function(htmlObject, e) {
  if (htmlObject && htmlObject.dragLanding) {
    if (this.lastLanding) {
      this.lastLanding.dragLanding._dragOut(this.lastLanding);
    }
    /** @type {!Object} */
    this.lastLanding = htmlObject;
    this.lastLanding = this.lastLanding.dragLanding._dragIn(this.lastLanding, this.dragStartNode, e.clientX, e.clientY, e);
    this.lastLanding_scr = _isIE ? e.srcElement : e.target;
  } else {
    if (htmlObject && "BODY" != htmlObject.tagName) {
      this.checkLanding(htmlObject.parentNode, e);
    } else {
      if (this.lastLanding) {
        this.lastLanding.dragLanding._dragOut(this.lastLanding, e.clientX, e.clientY, e);
      }
      /** @type {number} */
      this.lastLanding = 0;
      if (this._onNotFound) {
        this._onNotFound();
      }
    }
  }
}, dhtmlDragAndDropObject.prototype.stopDrag = function(e, silent) {
  var self = window.dhtmlDragAndDrop;
  if (!silent) {
    self.stopFrameRoute();
    var temp = self.lastLanding;
    /** @type {null} */
    self.lastLanding = null;
    if (temp) {
      temp.dragLanding._drag(self.dragStartNode, self.dragStartObject, temp, _isIE ? event.srcElement : e.target);
    }
  }
  /** @type {null} */
  self.lastLanding = null;
  if (self.dragNode && self.dragNode.parentNode == document.body) {
    self.dragNode.parentNode.removeChild(self.dragNode);
  }
  /** @type {number} */
  self.dragNode = 0;
  /** @type {number} */
  self.gldragNode = 0;
  /** @type {number} */
  self.fx = 0;
  /** @type {number} */
  self.fy = 0;
  /** @type {number} */
  self.dragStartNode = 0;
  /** @type {number} */
  self.dragStartObject = 0;
  document.body.onmouseup = self.tempDOMU;
  document.body.onmousemove = self.tempDOMM;
  /** @type {null} */
  self.tempDOMU = null;
  /** @type {null} */
  self.tempDOMM = null;
  /** @type {number} */
  self.waitDrag = 0;
}, dhtmlDragAndDropObject.prototype.stopFrameRoute = function(win) {
  if (win) {
    window.dhtmlDragAndDrop.stopDrag(1, 1);
  }
  /** @type {number} */
  var i = 0;
  for (; i < window.frames.length; i++) {
    try {
      if (window.frames[i] != win && window.frames[i].dhtmlDragAndDrop) {
        window.frames[i].dhtmlDragAndDrop.stopFrameRoute(window);
      }
    } catch (i) {
    }
  }
  try {
    if (parent.dhtmlDragAndDrop && parent != window && parent != win) {
      parent.dhtmlDragAndDrop.stopFrameRoute(window);
    }
  } catch (i) {
  }
}, dhtmlDragAndDropObject.prototype.initFrameRoute = function(win, mode) {
  if (win) {
    window.dhtmlDragAndDrop.preCreateDragCopy();
    window.dhtmlDragAndDrop.dragStartNode = win.dhtmlDragAndDrop.dragStartNode;
    window.dhtmlDragAndDrop.dragStartObject = win.dhtmlDragAndDrop.dragStartObject;
    window.dhtmlDragAndDrop.dragNode = win.dhtmlDragAndDrop.dragNode;
    window.dhtmlDragAndDrop.gldragNode = win.dhtmlDragAndDrop.dragNode;
    window.document.body.onmouseup = window.dhtmlDragAndDrop.stopDrag;
    /** @type {number} */
    window.waitDrag = 0;
    if (!_isIE && mode && (!_isFF || _FFrv < 1.8)) {
      window.dhtmlDragAndDrop.calculateFramePosition();
    }
  }
  try {
    if (parent.dhtmlDragAndDrop && parent != window && parent != win) {
      parent.dhtmlDragAndDrop.initFrameRoute(window);
    }
  } catch (i) {
  }
  /** @type {number} */
  var i = 0;
  for (; i < window.frames.length; i++) {
    try {
      if (window.frames[i] != win && window.frames[i].dhtmlDragAndDrop) {
        window.frames[i].dhtmlDragAndDrop.initFrameRoute(window, !win || mode ? 1 : 0);
      }
    } catch (i) {
    }
  }
}, _isFF = false, _isIE = false, _isOpera = false, _isKHTML = false, _isMacOS = false, _isChrome = false, _FFrv = false, _KHTMLrv = false, _OperaRv = false, -1 != navigator.userAgent.indexOf("Macintosh") && (_isMacOS = true), navigator.userAgent.toLowerCase().indexOf("chrome") > -1 && (_isChrome = true), -1 != navigator.userAgent.indexOf("Safari") || -1 != navigator.userAgent.indexOf("Konqueror") ? (_KHTMLrv = parseFloat(navigator.userAgent.substr(navigator.userAgent.indexOf("Safari") + 7, 5)), _KHTMLrv > 
525 ? (_isFF = true, _FFrv = 1.9) : _isKHTML = true) : -1 != navigator.userAgent.indexOf("Opera") ? (_isOpera = true, _OperaRv = parseFloat(navigator.userAgent.substr(navigator.userAgent.indexOf("Opera") + 6, 3))) : -1 != navigator.appName.indexOf("Microsoft") ? (_isIE = true, -1 == navigator.appVersion.indexOf("MSIE 8.0") && -1 == navigator.appVersion.indexOf("MSIE 9.0") && -1 == navigator.appVersion.indexOf("MSIE 10.0") || "BackCompat" == document.compatMode || (_isIE = 8)) : "Netscape" == navigator.appName && 
-1 != navigator.userAgent.indexOf("Trident") ? _isIE = 8 : (_isFF = true, _FFrv = parseFloat(navigator.userAgent.split("rv:")[1])), dtmlXMLLoaderObject.prototype.doXPath = function(xpathExp, docObj, namespace, result_type) {
  if (_isKHTML || !_isIE && !window.XPathResult) {
    return this.doXPathOpera(xpathExp, docObj);
  }
  if (_isIE) {
    return docObj || (docObj = this.xmlDoc.nodeName ? this.xmlDoc : this.xmlDoc.responseXML), docObj || dhtmlxError.throwError("LoadXML", "Incorrect XML", [docObj || this.xmlDoc, this.mainObject]), namespace && docObj.setProperty("SelectionNamespaces", "xmlns:xsl='" + namespace + "'"), "single" == result_type ? docObj.selectSingleNode(xpathExp) : docObj.selectNodes(xpathExp) || new Array(0);
  }
  /** @type {!Object} */
  var nodeObj = docObj;
  if (!docObj) {
    docObj = this.xmlDoc.nodeName ? this.xmlDoc : this.xmlDoc.responseXML;
  }
  if (!docObj) {
    dhtmlxError.throwError("LoadXML", "Incorrect XML", [docObj || this.xmlDoc, this.mainObject]);
  }
  if (-1 != docObj.nodeName.indexOf("document")) {
    /** @type {!Object} */
    nodeObj = docObj;
  } else {
    /** @type {!Object} */
    nodeObj = docObj;
    docObj = docObj.ownerDocument;
  }
  /** @type {number} */
  var retType = XPathResult.ANY_TYPE;
  if ("single" == result_type) {
    /** @type {number} */
    retType = XPathResult.FIRST_ORDERED_NODE_TYPE;
  }
  /** @type {!Array} */
  var rowsCol = [];
  var col = docObj.evaluate(xpathExp, nodeObj, function(canCreateDiscussions) {
    return namespace;
  }, retType, null);
  if (retType == XPathResult.FIRST_ORDERED_NODE_TYPE) {
    return col.singleNodeValue;
  }
  var thisColMemb = col.iterateNext();
  for (; thisColMemb;) {
    rowsCol[rowsCol.length] = thisColMemb;
    thisColMemb = col.iterateNext();
  }
  return rowsCol;
}, _dhtmlxError.prototype.catchError = function(type, func_name) {
  /** @type {!Function} */
  this.catches[type] = func_name;
}, _dhtmlxError.prototype.throwError = function(type, name, params) {
  return this.catches[type] ? this.catches[type](type, name, params) : this.catches.ALL ? this.catches.ALL(type, name, params) : (window.alert("Error type: " + arguments[0] + "\nDescription: " + arguments[1]), null);
}, window.dhtmlxError = new _dhtmlxError, dtmlXMLLoaderObject.prototype.doXPathOpera = function(xpathExp, docObj) {
  var z = xpathExp.replace(/[\/]+/gi, "/").split("/");
  /** @type {null} */
  var obj = null;
  /** @type {number} */
  var i = 1;
  if (!z.length) {
    return [];
  }
  if ("." == z[0]) {
    /** @type {!Array} */
    obj = [docObj];
  } else {
    if ("" !== z[0]) {
      return [];
    }
    obj = (this.xmlDoc.responseXML || this.xmlDoc).getElementsByTagName(z[i].replace(/\[[^\]]*\]/g, ""));
    i++;
  }
  i;
  for (; i < z.length; i++) {
    obj = this._getAllNamedChilds(obj, z[i]);
  }
  return -1 != z[i - 1].indexOf("[") && (obj = this._filterXPath(obj, z[i - 1])), obj;
}, dtmlXMLLoaderObject.prototype._filterXPath = function(a, b) {
  /** @type {!Array} */
  var c = [];
  b = b.replace(/[^\[]*\[@/g, "").replace(/[\[\]@]*/g, "");
  /** @type {number} */
  var i = 0;
  for (; i < a.length; i++) {
    if (a[i].getAttribute(b)) {
      c[c.length] = a[i];
    }
  }
  return c;
}, dtmlXMLLoaderObject.prototype._getAllNamedChilds = function(a, b) {
  /** @type {!Array} */
  var arr = [];
  if (_isKHTML) {
    b = b.toUpperCase();
  }
  /** @type {number} */
  var i = 0;
  for (; i < a.length; i++) {
    /** @type {number} */
    var i2 = 0;
    for (; i2 < a[i].childNodes.length; i2++) {
      if (_isKHTML) {
        if (a[i].childNodes[i2].tagName && a[i].childNodes[i2].tagName.toUpperCase() == b) {
          arr[arr.length] = a[i].childNodes[i2];
        }
      } else {
        if (a[i].childNodes[i2].tagName == b) {
          arr[arr.length] = a[i].childNodes[i2];
        }
      }
    }
  }
  return arr;
}, "undefined" == typeof window.dhtmlxEvent && (window.dhtmlxEvent = function(el, event, handler) {
  if (el.addEventListener) {
    el.addEventListener(event, handler, false);
  } else {
    if (el.attachEvent) {
      el.attachEvent("on" + event, handler);
    }
  }
}), dtmlXMLLoaderObject.prototype.xslDoc = null, dtmlXMLLoaderObject.prototype.setXSLParamValue = function(paramName, paramValue, xslDoc) {
  if (!xslDoc) {
    xslDoc = this.xslDoc;
  }
  if (xslDoc.responseXML) {
    xslDoc = xslDoc.responseXML;
  }
  var item = this.doXPath("/xsl:stylesheet/xsl:variable[@name='" + paramName + "']", xslDoc, "http://www.w3.org/1999/XSL/Transform", "single");
  if (item) {
    /** @type {string} */
    item.firstChild.nodeValue = paramValue;
  }
}, dtmlXMLLoaderObject.prototype.doXSLTransToObject = function(xslDoc, xmlDoc) {
  if (!xslDoc) {
    xslDoc = this.xslDoc;
  }
  if (xslDoc.responseXML) {
    xslDoc = xslDoc.responseXML;
  }
  if (!xmlDoc) {
    xmlDoc = this.xmlDoc;
  }
  if (xmlDoc.responseXML) {
    xmlDoc = xmlDoc.responseXML;
  }
  var result;
  if (_isIE) {
    result = new ActiveXObject("Msxml2.DOMDocument.3.0");
    try {
      xmlDoc.transformNodeToObject(xslDoc, result);
    } catch (r) {
      result = xmlDoc.transformNode(xslDoc);
    }
  } else {
    if (!this.XSLProcessor) {
      /** @type {!XSLTProcessor} */
      this.XSLProcessor = new XSLTProcessor;
      this.XSLProcessor.importStylesheet(xslDoc);
    }
    result = this.XSLProcessor.transformToDocument(xmlDoc);
  }
  return result;
}, dtmlXMLLoaderObject.prototype.doXSLTransToString = function(xslDoc, xmlDoc) {
  var res = this.doXSLTransToObject(xslDoc, xmlDoc);
  return "string" == typeof res ? res : this.doSerialization(res);
}, dtmlXMLLoaderObject.prototype.doSerialization = function(xmlDoc) {
  if (xmlDoc || (xmlDoc = this.xmlDoc), xmlDoc.responseXML && (xmlDoc = xmlDoc.responseXML), _isIE) {
    return xmlDoc.xml;
  }
  /** @type {!XMLSerializer} */
  var xmlSerializer = new XMLSerializer;
  return xmlSerializer.serializeToString(xmlDoc);
}, dhtmlxEventable = function(obj$jscomp$25) {
  /**
   * @param {string} name
   * @param {!Function} obj
   * @param {(Object|string)} event
   * @return {?}
   */
  obj$jscomp$25.attachEvent = function(name, obj, event) {
    return name = "ev_" + name.toLowerCase(), this[name] || (this[name] = new this.eventCatcher(event || this)), name + ":" + this[name].addEvent(obj);
  };
  /**
   * @param {string} evt
   * @param {!Array} elem
   * @return {?}
   */
  obj$jscomp$25.callEvent = function(evt, elem) {
    return evt = "ev_" + evt.toLowerCase(), this[evt] ? this[evt].apply(this, elem) : true;
  };
  /**
   * @param {string} f
   * @return {?}
   */
  obj$jscomp$25.checkEvent = function(f) {
    return !!this["ev_" + f.toLowerCase()];
  };
  /**
   * @param {?} obj$jscomp$26
   * @return {?}
   */
  obj$jscomp$25.eventCatcher = function(obj$jscomp$26) {
    /** @type {!Array} */
    var dhx_catch$jscomp$0 = [];
    /**
     * @return {?}
     */
    var z$jscomp$11 = function() {
      /** @type {boolean} */
      var res = true;
      /** @type {number} */
      var i = 0;
      for (; i < dhx_catch$jscomp$0.length; i++) {
        if (dhx_catch$jscomp$0[i]) {
          var zr = dhx_catch$jscomp$0[i].apply(obj$jscomp$26, arguments);
          res = res && zr;
        }
      }
      return res;
    };
    return z$jscomp$11.addEvent = function(ev$jscomp$0) {
      return "function" != typeof ev$jscomp$0 && (ev$jscomp$0 = eval(ev$jscomp$0)), ev$jscomp$0 ? dhx_catch$jscomp$0.push(ev$jscomp$0) - 1 : false;
    }, z$jscomp$11.removeEvent = function(id) {
      /** @type {null} */
      dhx_catch$jscomp$0[id] = null;
    }, z$jscomp$11;
  };
  /**
   * @param {string} event
   * @return {undefined}
   */
  obj$jscomp$25.detachEvent = function(event) {
    if (event) {
      var evt = event.split(":");
      this[evt[0]].removeEvent(evt[1]);
    }
  };
  /**
   * @return {undefined}
   */
  obj$jscomp$25.detachAllEvents = function() {
    var name;
    for (name in this) {
      if (0 === name.indexOf("ev_")) {
        this.detachEvent(name);
        /** @type {null} */
        this[name] = null;
      }
    }
  };
  /** @type {null} */
  obj$jscomp$25 = null;
}, scheduler.event = window.dhtmlxEvent, scheduler.eventRemove = function($elem, $type, $eventHandle) {
  if ($elem.removeEventListener) {
    $elem.removeEventListener($type, $eventHandle, false);
  } else {
    if ($elem.detachEvent) {
      $elem.detachEvent("on" + $type, $eventHandle);
    }
  }
}, function() {
  /**
   * @param {!Element} elem
   * @return {?}
   */
  function isHidden(elem) {
    /** @type {boolean} */
    var display = false;
    /** @type {boolean} */
    var value = false;
    if (window.getComputedStyle) {
      var style = window.getComputedStyle(elem, null);
      display = style.display;
      value = style.visibility;
    } else {
      if (elem.currentStyle) {
        display = elem.currentStyle.display;
        value = elem.currentStyle.visibility;
      }
    }
    /** @type {boolean} */
    var e = false;
    var n = scheduler._locate_css({
      target : elem
    }, "dhx_form_repeat", false);
    return n && (e = !("0px" != n.style.height)), e = e || !elem.offsetHeight, "none" != display && "hidden" != value && !e;
  }
  /**
   * @param {!Node} container
   * @return {?}
   */
  function getData(container) {
    return !isNaN(container.getAttribute("tabindex")) && 1 * container.getAttribute("tabindex") >= 0;
  }
  /**
   * @param {!Node} el
   * @return {?}
   */
  function makeDataBinding(el) {
    var knownElements = {
      a : true,
      area : true
    };
    return knownElements[el.nodeName.loLowerCase()] ? !!el.getAttribute("href") : true;
  }
  /**
   * @param {!Node} element
   * @return {?}
   */
  function getStyle(element) {
    var elementPropertyHandlers = {
      input : true,
      select : true,
      textarea : true,
      button : true,
      object : true
    };
    return elementPropertyHandlers[element.nodeName.toLowerCase()] ? !element.hasAttribute("disabled") : true;
  }
  /**
   * @param {!HTMLElement} module
   * @return {?}
   */
  scheduler._getFocusableNodes = function(module) {
    var elem = module.querySelectorAll(["a[href]", "area[href]", "input", "select", "textarea", "button", "iframe", "object", "embed", "[tabindex]", "[contenteditable]"].join(", "));
    /** @type {!Array<?>} */
    var block = Array.prototype.slice.call(elem, 0);
    /** @type {number} */
    var index = 0;
    for (; index < block.length; index++) {
      var node = block[index];
      var l = (getData(node) || getStyle(node) || makeDataBinding(node)) && isHidden(node);
      if (!l) {
        block.splice(index, 1);
        index--;
      }
    }
    return block;
  };
}(), scheduler._trim = function(lines) {
  /** @type {function(this:string): string} */
  var exports = String.prototype.trim || function() {
    return this.replace(/^\s+|\s+$/g, "");
  };
  return exports.apply(lines);
}, scheduler._isDate = function(value) {
  return value && "object" == typeof value ? !!(value.getFullYear && value.getMonth && value.getDate) : false;
}, scheduler._isObject = function(data) {
  return data && "object" == typeof data;
}, window.dhtmlx || (window.dhtmlx = {}), function() {
  /**
   * @param {!Object} options
   * @param {string} e
   * @return {undefined}
   */
  function init(options, e) {
    setTimeout(function() {
      if (options.box) {
        var callback = options.callback;
        modality(false);
        options.box.parentNode.removeChild(options.box);
        dhtmlx.callEvent("onAfterMessagePopup", [options.box]);
        /** @type {null} */
        mockOptions = options.box = null;
        if (callback) {
          callback(e);
        }
      }
    }, 1);
  }
  /**
   * @param {!Object} e
   * @return {?}
   */
  function handler(e) {
    if (mockOptions) {
      e = e || event;
      var j = e.which || event.keyCode;
      /** @type {boolean} */
      var r = false;
      if (dhtmlx.message.keyboard) {
        if (13 == j || 32 == j) {
          var source = e.target || e.srcElement;
          if (scheduler._getClassName(source).indexOf("dhtmlx_popup_button") > -1 && source.click) {
            source.click();
          } else {
            init(mockOptions, true);
            /** @type {boolean} */
            r = true;
          }
        }
        if (27 == j) {
          init(mockOptions, false);
          /** @type {boolean} */
          r = true;
        }
      }
      if (r) {
        return e.preventDefault && e.preventDefault(), !(e.cancelBubble = true);
      }
    } else {
    }
  }
  /**
   * @param {boolean} mode
   * @return {undefined}
   */
  function modality(mode) {
    if (!modality.cover) {
      /** @type {!Element} */
      modality.cover = document.createElement("div");
      /** @type {function(!Object): ?} */
      modality.cover.onkeydown = handler;
      /** @type {string} */
      modality.cover.className = "dhx_modal_cover";
      document.body.appendChild(modality.cover);
    }
    document.body.scrollHeight;
    /** @type {string} */
    modality.cover.style.display = mode ? "inline-block" : "none";
  }
  /**
   * @param {!Object} e
   * @param {number} _
   * @param {!Object} val
   * @return {?}
   */
  function log(e, _, val) {
    var this_area = scheduler._waiAria.messageButtonAttrString(e);
    var tmp = val ? val : e || "";
    /** @type {string} */
    var CLS_UPLOADER_BUTTON = "dhtmlx_" + tmp.toLowerCase().replace(/ /g, "_") + "_button";
    return "<div " + this_area + "class='dhtmlx_popup_button " + CLS_UPLOADER_BUTTON + "' result='" + _ + "' ><div>" + e + "</div></div>";
  }
  /**
   * @param {string} text
   * @return {?}
   */
  function info(text) {
    if (!self.area) {
      /** @type {!Element} */
      self.area = document.createElement("div");
      /** @type {string} */
      self.area.className = "dhtmlx_message_area";
      /** @type {string} */
      self.area.style[self.position] = "5px";
      document.body.appendChild(self.area);
    }
    self.hide(text.id);
    /** @type {!Element} */
    var e = document.createElement("div");
    return e.innerHTML = "<div>" + text.text + "</div>", e.className = "dhtmlx-info dhtmlx-" + text.type, e.onclick = function() {
      self.hide(text.id);
      /** @type {null} */
      text = null;
    }, scheduler._waiAria.messageInfoAttr(e), "bottom" == self.position && self.area.firstChild ? self.area.insertBefore(e, self.area.firstChild) : self.area.appendChild(e), text.expire > 0 && (self.timers[text.id] = window.setTimeout(function() {
      self.hide(text.id);
    }, text.expire)), self.pull[text.id] = e, e = null, text.id;
  }
  /**
   * @param {!Object} config
   * @param {boolean} ok
   * @param {boolean} cancel
   * @return {?}
   */
  function _boxStructure(config, ok, cancel) {
    /** @type {!Element} */
    var box = document.createElement("div");
    /** @type {string} */
    box.className = " dhtmlx_modal_box dhtmlx-" + config.type;
    box.setAttribute("dhxbox", 1);
    var t0uv = scheduler.uid();
    scheduler._waiAria.messageModalAttr(box, t0uv);
    /** @type {string} */
    var x = "";
    /** @type {boolean} */
    var t = false;
    if (config.width && (box.style.width = config.width), config.height && (box.style.height = config.height), config.title && (x = x + ('<div class="dhtmlx_popup_title" id="' + t0uv + '">' + config.title + "</div>"), t = true), x = x + ('<div class="dhtmlx_popup_text" ' + (t ? "" : ' id="' + t0uv + '" ') + "><span>" + (config.content ? "" : config.text) + '</span></div><div  class="dhtmlx_popup_controls">'), ok) {
      var params = config.ok || scheduler.locale.labels.message_ok;
      if (void 0 === params) {
        /** @type {string} */
        params = "OK";
      }
      /** @type {string} */
      x = x + log(params, true, "ok");
    }
    if (cancel) {
      var params = config.cancel || scheduler.locale.labels.message_cancel;
      if (void 0 === params) {
        /** @type {string} */
        params = "Cancel";
      }
      /** @type {string} */
      x = x + log(params, false, "cancel");
    }
    if (config.buttons) {
      /** @type {number} */
      var i = 0;
      for (; i < config.buttons.length; i++) {
        /** @type {string} */
        x = x + log(config.buttons[i], i);
      }
    }
    if (x = x + "</div>", box.innerHTML = x, config.content) {
      var el = config.content;
      if ("string" == typeof el) {
        /** @type {(Element|null)} */
        el = document.getElementById(el);
      }
      if ("none" == el.style.display) {
        /** @type {string} */
        el.style.display = "";
      }
      box.childNodes[config.title ? 1 : 0].appendChild(el);
    }
    return box.onclick = function(e) {
      e = e || event;
      var td = e.target || e.srcElement;
      var col2 = scheduler._getClassName(td);
      if (col2 || (td = td.parentNode), col2 = scheduler._getClassName(td), "dhtmlx_popup_button" == col2.split(" ")[0]) {
        var id = td.getAttribute("result");
        id = "true" == id || ("false" == id ? false : id);
        init(config, id);
      }
    }, config.box = box, mockOptions = config, box;
  }
  /**
   * @param {!Object} config
   * @param {boolean} ok
   * @param {boolean} cancel
   * @return {?}
   */
  function _createBox(config, ok, cancel) {
    var node = config.tagName ? config : _boxStructure(config, ok, cancel);
    if (!config.hidden) {
      modality(true);
    }
    document.body.appendChild(node);
    /** @type {number} */
    var targetL = Math.abs(Math.floor(((window.innerWidth || document.documentElement.offsetWidth) - node.offsetWidth) / 2));
    /** @type {number} */
    var y_body_bottom = Math.abs(Math.floor(((window.innerHeight || document.documentElement.offsetHeight) - node.offsetHeight) / 2));
    return "top" == config.position ? node.style.top = "-3px" : node.style.top = y_body_bottom + "px", node.style.left = targetL + "px", node.onkeydown = handler, dhtmlx.modalbox.focus(node), config.hidden && dhtmlx.modalbox.hide(node), dhtmlx.callEvent("onMessagePopup", [node]), node;
  }
  /**
   * @param {string} config
   * @return {?}
   */
  function boxPopup(config) {
    return _createBox(config, true, false);
  }
  /**
   * @param {string} config
   * @return {?}
   */
  function alertPopup(config) {
    return _createBox(config, true, true);
  }
  /**
   * @param {string} config
   * @return {?}
   */
  function confirmPopup(config) {
    return _createBox(config);
  }
  /**
   * @param {!Object} item
   * @param {string} n
   * @param {!Object} c
   * @return {?}
   */
  function h(item, n, c) {
    return "object" != typeof item && ("function" == typeof n && (c = n, n = ""), item = {
      text : item,
      type : n,
      callback : c
    }), item;
  }
  /**
   * @param {!Object} text
   * @param {string} t
   * @param {number} data
   * @param {string} userId
   * @return {?}
   */
  function setup(text, t, data, userId) {
    return "object" != typeof text && (text = {
      text : text,
      type : t,
      expire : data,
      id : userId
    }), text.id = text.id || self.uid(), text.expire = text.expire || self.expire, text;
  }
  /** @type {null} */
  var mockOptions = null;
  if (document.attachEvent) {
    document.attachEvent("onkeydown", handler);
  } else {
    document.addEventListener("keydown", handler, true);
  }
  /**
   * @return {?}
   */
  dhtmlx.alert = function() {
    var text = h.apply(this, arguments);
    return text.type = text.type || "confirm", boxPopup(text);
  };
  /**
   * @return {?}
   */
  dhtmlx.confirm = function() {
    var text = h.apply(this, arguments);
    return text.type = text.type || "alert", alertPopup(text);
  };
  /**
   * @return {?}
   */
  dhtmlx.modalbox = function() {
    var text = h.apply(this, arguments);
    return text.type = text.type || "alert", confirmPopup(text);
  };
  /**
   * @param {!Object} node
   * @return {undefined}
   */
  dhtmlx.modalbox.hide = function(node) {
    for (; node && node.getAttribute && !node.getAttribute("dhxbox");) {
      node = node.parentNode;
    }
    if (node) {
      node.parentNode.removeChild(node);
      modality(false);
    }
  };
  /**
   * @param {!HTMLElement} link
   * @return {undefined}
   */
  dhtmlx.modalbox.focus = function(link) {
    setTimeout(function() {
      var children = scheduler._getFocusableNodes(link);
      if (children.length && children[0].focus) {
        children[0].focus();
      }
    }, 1);
  };
  /** @type {function(string, ?, ?, ?): ?} */
  var self = dhtmlx.message = function(text, module, attrName, opt_errorDetails) {
    text = setup.apply(this, arguments);
    text.type = text.type || "info";
    var subtype = text.type.split("-")[0];
    switch(subtype) {
      case "alert":
        return boxPopup(text);
      case "confirm":
        return alertPopup(text);
      case "modalbox":
        return confirmPopup(text);
      default:
        return info(text);
    }
  };
  /** @type {number} */
  self.seed = (new Date).valueOf();
  /**
   * @return {?}
   */
  self.uid = function() {
    return self.seed++;
  };
  /** @type {number} */
  self.expire = 4e3;
  /** @type {boolean} */
  self.keyboard = true;
  /** @type {string} */
  self.position = "top";
  self.pull = {};
  self.timers = {};
  /**
   * @return {undefined}
   */
  self.hideAll = function() {
    var key;
    for (key in self.pull) {
      self.hide(key);
    }
  };
  /**
   * @param {string} id
   * @return {undefined}
   */
  self.hide = function(id) {
    var t = self.pull[id];
    if (t && t.parentNode) {
      window.setTimeout(function() {
        t.parentNode.removeChild(t);
        /** @type {null} */
        t = null;
      }, 2e3);
      t.className += " hidden";
      if (self.timers[id]) {
        window.clearTimeout(self.timers[id]);
      }
      delete self.pull[id];
    }
  };
}(), dhtmlx.attachEvent || dhtmlxEventable(dhtmlx);
/** @type {function(string): ?} */
var dataProcessor = window.dataProcessor = function(file) {
  return this.serverProcessor = file, this.action_param = "!nativeeditor_status", this.object = null, this.updatedRows = [], this.autoUpdate = true, this.updateMode = "cell", this._tMode = "GET", this._headers = null, this._payload = null, this.post_delim = "_", this._waitMode = 0, this._in_progress = {}, this._invalid = {}, this.mandatoryFields = [], this.messages = [], this.styles = {
    updated : "font-weight:bold;",
    inserted : "font-weight:bold;",
    deleted : "text-decoration : line-through;",
    invalid : "background-color:FFE0E0;",
    invalid_cell : "border-bottom:2px solid red;",
    error : "color:red;",
    clear : "font-weight:normal;text-decoration:none;"
  }, this.enableUTFencoding(true), dhtmlxEventable(this), this;
};
dataProcessor.prototype = {
  setTransactionMode : function(options, anyContent) {
    if ("object" == typeof options) {
      this._tMode = options.mode || this._tMode;
      if (void 0 !== options.headers) {
        this._headers = options.headers;
      }
      if (void 0 !== options.payload) {
        this._payload = options.payload;
      }
    } else {
      /** @type {!Object} */
      this._tMode = options;
      /** @type {boolean} */
      this._tSend = anyContent;
    }
    if ("REST" == this._tMode) {
      /** @type {boolean} */
      this._tSend = false;
      /** @type {boolean} */
      this._endnm = true;
    }
    if ("JSON" == this._tMode) {
      /** @type {boolean} */
      this._tSend = false;
      /** @type {boolean} */
      this._endnm = true;
      this._headers = this._headers || {};
      /** @type {string} */
      this._headers["Content-type"] = "application/json";
    }
  },
  escape : function(s) {
    return this._utf ? encodeURIComponent(s) : escape(s);
  },
  enableUTFencoding : function(zoomAware) {
    /** @type {boolean} */
    this._utf = !!zoomAware;
  },
  setDataColumns : function(n) {
    this._columns = "string" == typeof n ? n.split(",") : n;
  },
  getSyncState : function() {
    return !this.updatedRows.length;
  },
  enableDataNames : function(canCreateDiscussions) {
    /** @type {boolean} */
    this._endnm = !!canCreateDiscussions;
  },
  enablePartialDataSend : function(canCreateDiscussions) {
    /** @type {boolean} */
    this._changed = !!canCreateDiscussions;
  },
  setUpdateMode : function(undefined, mode) {
    /** @type {boolean} */
    this.autoUpdate = "cell" == undefined;
    /** @type {string} */
    this.updateMode = undefined;
    /** @type {!File} */
    this.dnd = mode;
  },
  ignore : function(fn, ctx) {
    /** @type {boolean} */
    this._silent_mode = true;
    fn.call(ctx || window);
    /** @type {boolean} */
    this._silent_mode = false;
  },
  setUpdated : function(id, property, type) {
    if (!this._silent_mode) {
      var row = this.findRow(id);
      type = type || "updated";
      var node = this.obj.getUserData(id, this.action_param);
      if (node && "updated" == type) {
        type = node;
      }
      if (property) {
        this.set_invalid(id, false);
        /** @type {boolean} */
        this.updatedRows[row] = id;
        this.obj.setUserData(id, this.action_param, type);
        if (this._in_progress[id]) {
          /** @type {string} */
          this._in_progress[id] = "wait";
        }
      } else {
        if (!this.is_invalid(id)) {
          this.updatedRows.splice(row, 1);
          this.obj.setUserData(id, this.action_param, "");
        }
      }
      if (!property) {
        this._clearUpdateFlag(id);
      }
      this.markRow(id, property, type);
      if (property && this.autoUpdate) {
        this.sendData(id);
      }
    }
  },
  _clearUpdateFlag : function(studentId) {
  },
  markRow : function(val, parent, name) {
    /** @type {string} */
    var node = "";
    var v = this.is_invalid(val);
    if (v && (node = this.styles[v], parent = true), this.callEvent("onRowMark", [val, parent, name, v]) && (node = this.styles[parent ? name : "clear"] + node, this.obj[this._methods[0]](val, node), v && v.details)) {
      node = node + this.styles[v + "_cell"];
      /** @type {number} */
      var i = 0;
      for (; i < v.details.length; i++) {
        if (v.details[i]) {
          this.obj[this._methods[1]](val, i, node);
        }
      }
    }
  },
  getState : function(id) {
    return this.obj.getUserData(id, this.action_param);
  },
  is_invalid : function(key) {
    return this._invalid[key];
  },
  set_invalid : function(path, data, torrentname) {
    if (torrentname) {
      data = {
        value : data,
        details : torrentname,
        toString : function() {
          return this.value.toString();
        }
      };
    }
    /** @type {string} */
    this._invalid[path] = data;
  },
  checkBeforeUpdate : function(lookupCharacterIndex) {
    return true;
  },
  sendData : function(index) {
    return !this._waitMode || "tree" != this.obj.mytype && !this.obj._h2 ? (this.obj.editStop && this.obj.editStop(), "undefined" == typeof index || this._tSend ? this.sendAllData() : this._in_progress[index] ? false : (this.messages = [], !this.checkBeforeUpdate(index) && this.callEvent("onValidationError", [index, this.messages]) ? false : void this._beforeSendData(this._getRowData(index), index))) : void 0;
  },
  _beforeSendData : function(value, i) {
    return this.callEvent("onBeforeUpdate", [i, this.getState(i), value]) ? void this._sendData(value, i) : false;
  },
  serialize : function(o, value) {
    if ("string" == typeof o) {
      return o;
    }
    if ("undefined" != typeof value) {
      return this.serialize_one(o, "");
    }
    /** @type {!Array} */
    var drilldownLevelLabels = [];
    /** @type {!Array} */
    var arrUrls = [];
    var t;
    for (t in o) {
      if (o.hasOwnProperty(t)) {
        drilldownLevelLabels.push(this.serialize_one(o[t], t + this.post_delim));
        arrUrls.push(t);
      }
    }
    return drilldownLevelLabels.push("ids=" + this.escape(arrUrls.join(","))), dhtmlx.security_key && drilldownLevelLabels.push("dhx_security=" + dhtmlx.security_key), drilldownLevelLabels.join("&");
  },
  serialize_one : function(values, prefix) {
    if ("string" == typeof values) {
      return values;
    }
    /** @type {!Array} */
    var drilldownLevelLabels = [];
    var value;
    for (value in values) {
      if (values.hasOwnProperty(value)) {
        if (("id" == value || value == this.action_param) && "REST" == this._tMode) {
          continue;
        }
        drilldownLevelLabels.push(this.escape((prefix || "") + value) + "=" + this.escape(values[value]));
      }
    }
    return drilldownLevelLabels.join("&");
  },
  _applyPayload : function(key) {
    var nodes = this.obj.$ajax;
    if (this._payload) {
      var i;
      for (i in this._payload) {
        key = key + nodes.urlSeparator(key) + this.escape(i) + "=" + this.escape(this._payload[i]);
      }
    }
    return key;
  },
  _sendData : function(value, type) {
    if (value) {
      if (!this.callEvent("onBeforeDataSending", type ? [type, this.getState(type), value] : [null, null, value])) {
        return false;
      }
      if (type) {
        /** @type {number} */
        this._in_progress[type] = (new Date).valueOf();
      }
      var self = this;
      /**
       * @param {string} value
       * @return {?}
       */
      var success = function(value) {
        /** @type {!Array} */
        var options = [];
        if (type) {
          options.push(type);
        } else {
          if (value) {
            var index;
            for (index in value) {
              options.push(index);
            }
          }
        }
        return self.afterUpdate(self, value, options);
      };
      var $ = this.obj.$ajax;
      var a = this.serverProcessor + (this._user ? $.urlSeparator(this.serverProcessor) + ["dhx_user=" + this._user, "dhx_version=" + this.obj.getUserData(0, "version")].join("&") : "");
      var key = this._applyPayload(a);
      if ("GET" == this._tMode) {
        $.query({
          url : key + $.urlSeparator(key) + this.serialize(value, type),
          method : "GET",
          callback : success,
          headers : this._headers
        });
      } else {
        if ("POST" == this._tMode) {
          $.query({
            url : key,
            method : "POST",
            headers : this._headers,
            data : this.serialize(value, type),
            callback : success
          });
        } else {
          if ("JSON" == this._tMode) {
            var url = value[this.action_param];
            var data = {};
            var k;
            for (k in value) {
              data[k] = value[k];
            }
            delete data[this.action_param];
            delete data.id;
            delete data.gr_id;
            $.query({
              url : key,
              method : "POST",
              headers : this._headers,
              callback : success,
              data : JSON.stringify({
                id : type,
                action : url,
                data : data
              })
            });
          } else {
            if ("REST" == this._tMode) {
              var state = this.getState(type);
              var path = a.replace(/(&|\?)editing=true/, "");
              /** @type {string} */
              data = "";
              /** @type {string} */
              var method = "post";
              if ("inserted" == state) {
                data = this.serialize(value, type);
              } else {
                if ("deleted" == state) {
                  /** @type {string} */
                  method = "DELETE";
                  /** @type {string} */
                  path = path + ("/" == path.slice(-1) ? "" : "/") + type;
                } else {
                  /** @type {string} */
                  method = "PUT";
                  data = this.serialize(value, type);
                  /** @type {string} */
                  path = path + ("/" == path.slice(-1) ? "" : "/") + type;
                }
              }
              path = this._applyPayload(path);
              $.query({
                url : path,
                method : method,
                headers : this._headers,
                data : data,
                callback : success
              });
            }
          }
        }
      }
      this._waitMode++;
    }
  },
  sendAllData : function() {
    if (this.updatedRows.length) {
      /** @type {!Array} */
      this.messages = [];
      /** @type {boolean} */
      var a = true;
      /** @type {number} */
      var layer_i = 0;
      for (; layer_i < this.updatedRows.length; layer_i++) {
        /** @type {number} */
        a = a & this.checkBeforeUpdate(this.updatedRows[layer_i]);
      }
      if (!a && !this.callEvent("onValidationError", ["", this.messages])) {
        return false;
      }
      if (this._tSend) {
        this._sendData(this._getAllData());
      } else {
        /** @type {number} */
        layer_i = 0;
        for (; layer_i < this.updatedRows.length; layer_i++) {
          if (!this._in_progress[this.updatedRows[layer_i]]) {
            if (this.is_invalid(this.updatedRows[layer_i])) {
              continue;
            }
            if (this._beforeSendData(this._getRowData(this.updatedRows[layer_i]), this.updatedRows[layer_i]), this._waitMode && ("tree" == this.obj.mytype || this.obj._h2)) {
              return;
            }
          }
        }
      }
    }
  },
  _getAllData : function(canCreateDiscussions) {
    var ip = {};
    /** @type {boolean} */
    var vm_enabled = false;
    /** @type {number} */
    var _i = 0;
    for (; _i < this.updatedRows.length; _i++) {
      var i = this.updatedRows[_i];
      if (!this._in_progress[i] && !this.is_invalid(i)) {
        var value = this._getRowData(i);
        if (this.callEvent("onBeforeUpdate", [i, this.getState(i), value])) {
          ip[i] = value;
          /** @type {boolean} */
          vm_enabled = true;
          /** @type {number} */
          this._in_progress[i] = (new Date).valueOf();
        }
      }
    }
    return vm_enabled ? ip : null;
  },
  setVerificator : function(index, value) {
    this.mandatoryFields[index] = value || function(value) {
      return "" !== value;
    };
  },
  clearVerificator : function(index) {
    /** @type {boolean} */
    this.mandatoryFields[index] = false;
  },
  findRow : function(doc) {
    /** @type {number} */
    var i = 0;
    /** @type {number} */
    i = 0;
    for (; i < this.updatedRows.length && doc != this.updatedRows[i]; i++) {
    }
    return i;
  },
  defineAction : function(action, callback) {
    if (!this._uActions) {
      /** @type {!Array} */
      this._uActions = [];
    }
    this._uActions[action] = callback;
  },
  afterUpdateCallback : function(id, value, type, instance) {
    /** @type {boolean} */
    var junctorPK = id;
    /** @type {boolean} */
    var result = "error" != type && "invalid" != type;
    if (result || this.set_invalid(id, type), this._uActions && this._uActions[type] && !this._uActions[type](instance)) {
      return delete this._in_progress[junctorPK];
    }
    if ("wait" != this._in_progress[junctorPK]) {
      this.setUpdated(id, false);
    }
    /** @type {boolean} */
    var i = id;
    switch(type) {
      case "inserted":
      case "insert":
        if (value != id) {
          this.setUpdated(id, false);
          this.obj[this._methods[2]](id, value);
          /** @type {boolean} */
          id = value;
        }
        break;
      case "delete":
      case "deleted":
        return this.obj.setUserData(id, this.action_param, "true_deleted"), this.obj[this._methods[3]](id, value), delete this._in_progress[junctorPK], this.callEvent("onAfterUpdate", [id, type, value, instance]);
    }
    if ("wait" != this._in_progress[junctorPK]) {
      if (result) {
        this.obj.setUserData(id, this.action_param, "");
      }
      delete this._in_progress[junctorPK];
    } else {
      delete this._in_progress[junctorPK];
      this.setUpdated(value, true, this.obj.getUserData(id, this.action_param));
    }
    this.callEvent("onAfterUpdate", [i, type, value, instance]);
  },
  _errorResponse : function(t, data) {
    return this.obj && this.obj.callEvent && this.obj.callEvent("onSaveError", [data, t.xmlDoc]), this.cleanUpdate(data);
  },
  afterUpdate : function(fn, t, options) {
    var m = this.obj.$ajax;
    if (200 !== t.xmlDoc.status) {
      return void this._errorResponse(t, options);
    }
    if (window.JSON) {
      var o;
      try {
        /** @type {*} */
        o = JSON.parse(t.xmlDoc.responseText);
      } catch (a) {
        if (!t.xmlDoc.responseText.length) {
          o = {};
        }
      }
      if (o) {
        var elem = o.action || this.getState(options) || "updated";
        var s = o.sid || options[0];
        var tx = o.tid || options[0];
        return fn.afterUpdateCallback(s, tx, elem, o), void fn.finalizeUpdate();
      }
    }
    var path = m.xmltop("data", t.xmlDoc);
    if (!path) {
      return this._errorResponse(t, options);
    }
    var triangle = m.xpath("//data/action", path);
    if (!triangle.length) {
      this._errorResponse(t, options);
    }
    /** @type {number} */
    var i = 0;
    for (; i < triangle.length; i++) {
      var a = triangle[i];
      elem = a.getAttribute("type");
      s = a.getAttribute("sid");
      tx = a.getAttribute("tid");
      fn.afterUpdateCallback(s, tx, elem, a);
    }
    fn.finalizeUpdate();
  },
  cleanUpdate : function(Uint16s) {
    if (Uint16s) {
      /** @type {number} */
      var i = 0;
      for (; i < Uint16s.length; i++) {
        delete this._in_progress[Uint16s[i]];
      }
    }
  },
  finalizeUpdate : function() {
    if (this._waitMode) {
      this._waitMode--;
    }
    if (("tree" == this.obj.mytype || this.obj._h2) && this.updatedRows.length) {
      this.sendData();
    }
    this.callEvent("onAfterUpdateFinish", []);
    if (!this.updatedRows.length) {
      this.callEvent("onFullSync", []);
    }
  },
  init : function(object) {
    /** @type {!Object} */
    this.obj = object;
    if (this.obj._dp_init) {
      this.obj._dp_init(this);
    }
  },
  setOnAfterUpdate : function(fn) {
    this.attachEvent("onAfterUpdate", fn);
  },
  enableDebug : function(bool) {
  },
  setOnBeforeUpdateHandler : function(fn) {
    this.attachEvent("onBeforeDataSending", fn);
  },
  setAutoUpdate : function(event, user) {
    event = event || 2e3;
    this._user = user || (new Date).valueOf();
    /** @type {boolean} */
    this._need_update = false;
    /** @type {boolean} */
    this._update_busy = false;
    this.attachEvent("onAfterUpdate", function(e, 1, i, forceOptional) {
      this.afterAutoUpdate(e, 1, i, forceOptional);
    });
    this.attachEvent("onFullSync", function() {
      this.fullSync();
    });
    var i = this;
    window.setInterval(function() {
      i.loadUpdate();
    }, event);
  },
  afterAutoUpdate : function(e, islongclick, i, forceOptional) {
    return "collision" == islongclick ? (this._need_update = true, false) : true;
  },
  fullSync : function() {
    return this._need_update && (this._need_update = false, this.loadUpdate()), true;
  },
  getUpdates : function(data, path) {
    var texture = this.obj.$ajax;
    return this._update_busy ? false : (this._update_busy = true, void texture.get(data, path));
  },
  _v : function(node) {
    return node.firstChild ? node.firstChild.nodeValue : "";
  },
  _a : function(msg) {
    /** @type {!Array} */
    var node = [];
    /** @type {number} */
    var t = 0;
    for (; t < msg.length; t++) {
      node[t] = this._v(msg[t]);
    }
    return node;
  },
  loadUpdate : function() {
    var element = this.obj.$ajax;
    var self = this;
    var vfXpub = this.obj.getUserData(0, "version");
    /** @type {string} */
    var r = this.serverProcessor + element.urlSeparator(this.serverProcessor) + ["dhx_user=" + this._user, "dhx_version=" + vfXpub].join("&");
    /** @type {string} */
    r = r.replace("editing=true&", "");
    this.getUpdates(r, function(path) {
      var collection = element.xpath("//userdata", path);
      self.obj.setUserData(0, "version", self._v(collection[0]));
      var hexNodes = element.xpath("//update", path);
      if (hexNodes.length) {
        /** @type {boolean} */
        self._silent_mode = true;
        /** @type {number} */
        var i = 0;
        for (; i < hexNodes.length; i++) {
          var cmd = hexNodes[i].getAttribute("status");
          var ind = hexNodes[i].getAttribute("id");
          var parent_id = hexNodes[i].getAttribute("parent");
          switch(cmd) {
            case "inserted":
              self.callEvent("insertCallback", [hexNodes[i], ind, parent_id]);
              break;
            case "updated":
              self.callEvent("updateCallback", [hexNodes[i], ind, parent_id]);
              break;
            case "deleted":
              self.callEvent("deleteCallback", [hexNodes[i], ind, parent_id]);
          }
        }
        /** @type {boolean} */
        self._silent_mode = false;
      }
      /** @type {boolean} */
      self._update_busy = false;
      /** @type {null} */
      self = null;
    });
  }
}, window.dataProcessor && !dataProcessor.prototype.init_original && (dataProcessor.prototype.init_original = dataProcessor.prototype.init, dataProcessor.prototype.init = function(obj) {
  this.init_original(obj);
  obj._dataprocessor = this;
  this.setTransactionMode("POST", true);
  this.serverProcessor += (-1 != this.serverProcessor.indexOf("?") ? "&" : "?") + "editing=true";
}), dhtmlxError.catchError("LoadXML", function(canCreateDiscussions, isSlidingUp, reqs) {
  var errorText = reqs[0].responseText;
  switch(scheduler.config.ajax_error) {
    case "alert":
      window.alert(errorText);
      break;
    case "console":
      window.console.log(errorText);
  }
}), function() {
  /**
   * @param {string} data
   * @return {?}
   */
  function convert(data) {
    return (data + "").replace(regExp, " ").replace(regexp, " ");
  }
  /**
   * @param {string} expression
   * @return {?}
   */
  function fn(expression) {
    return (expression + "").replace(reg, "&#39;");
  }
  /**
   * @return {?}
   */
  function listStarterkits() {
    return !scheduler.config.wai_aria_attributes;
  }
  /** @type {!RegExp} */
  var regExp = new RegExp("<(?:.|\n)*?>", "gm");
  /** @type {!RegExp} */
  var regexp = new RegExp(" +", "gm");
  /** @type {!RegExp} */
  var reg = new RegExp("'", "gm");
  scheduler._waiAria = {
    getAttributeString : function(data) {
      /** @type {!Array} */
      var drilldownLevelLabels = [" "];
      var i;
      for (i in data) {
        if ("function" != typeof data[i] && "object" != typeof data[i]) {
          var n = fn(convert(data[i]));
          drilldownLevelLabels.push(i + "='" + n + "'");
        }
      }
      return drilldownLevelLabels.push(" "), drilldownLevelLabels.join(" ");
    },
    setAttributes : function(node, data) {
      var k;
      for (k in data) {
        node.setAttribute(k, convert(data[k]));
      }
      return node;
    },
    labelAttr : function(obj, text) {
      return this.setAttributes(obj, {
        "aria-label" : text
      });
    },
    label : function(label) {
      return scheduler._waiAria.getAttributeString({
        "aria-label" : label
      });
    },
    hourScaleAttr : function(row, tagName) {
      this.labelAttr(row, tagName);
    },
    monthCellAttr : function(section, date) {
      this.labelAttr(section, scheduler.templates.day_date(date));
    },
    navBarDateAttr : function(innerErrors, message) {
      this.labelAttr(innerErrors, message);
    },
    dayHeaderAttr : function(prop, desc) {
      this.labelAttr(prop, desc);
    },
    dayColumnAttr : function(status, date) {
      this.dayHeaderAttr(status, scheduler.templates.day_date(date));
    },
    headerButtonsAttributes : function(size, text) {
      return this.setAttributes(size, {
        role : "button",
        "aria-label" : text
      });
    },
    headerToggleState : function(obj, multiple) {
      return this.setAttributes(obj, {
        "aria-pressed" : multiple ? "true" : "false"
      });
    },
    getHeaderCellAttr : function(ariaLabel) {
      return scheduler._waiAria.getAttributeString({
        "aria-label" : ariaLabel
      });
    },
    eventAttr : function(text, obj) {
      this._eventCommonAttr(text, obj);
    },
    _eventCommonAttr : function(data, node) {
      node.setAttribute("aria-label", convert(scheduler.templates.event_text(data.start_date, data.end_date, data)));
      if (scheduler.config.readonly) {
        node.setAttribute("aria-readonly", true);
      }
      if (data.$dataprocessor_class) {
        node.setAttribute("aria-busy", true);
      }
      node.setAttribute("aria-selected", scheduler.getState().select_id == data.id ? "true" : "false");
    },
    setEventBarAttr : function(configData, next) {
      this._eventCommonAttr(configData, next);
    },
    _getAttributes : function(fn, obj) {
      var element = {
        setAttribute : function(attr, key) {
          /** @type {string} */
          this[attr] = key;
        }
      };
      return fn.apply(this, [obj, element]), element;
    },
    eventBarAttrString : function(ss) {
      return this.getAttributeString(this._getAttributes(this.setEventBarAttr, ss));
    },
    agendaHeadAttrString : function() {
      return this.getAttributeString({
        role : "row"
      });
    },
    agendaHeadDateString : function(ariaLabel) {
      return this.getAttributeString({
        role : "columnheader",
        "aria-label" : ariaLabel
      });
    },
    agendaHeadDescriptionString : function(ariaLabel) {
      return this.agendaHeadDateString(ariaLabel);
    },
    agendaDataAttrString : function() {
      return this.getAttributeString({
        role : "grid"
      });
    },
    agendaEventAttrString : function(selector) {
      var rule = this._getAttributes(this._eventCommonAttr, selector);
      return rule.role = "row", this.getAttributeString(rule);
    },
    agendaDetailsBtnString : function() {
      return this.getAttributeString({
        role : "button",
        "aria-label" : scheduler.locale.labels.icon_details
      });
    },
    gridAttrString : function() {
      return this.getAttributeString({
        role : "grid"
      });
    },
    gridRowAttrString : function(whitelistSelector) {
      return this.agendaEventAttrString(whitelistSelector);
    },
    gridCellAttrString : function(cond, t, i) {
      return this.getAttributeString({
        role : "gridcell",
        "aria-label" : [void 0 === t.label ? t.id : t.label, ": ", i]
      });
    },
    mapAttrString : function() {
      return this.gridAttrString();
    },
    mapRowAttrString : function(leftFence) {
      return this.gridRowAttrString(leftFence);
    },
    mapDetailsBtnString : function() {
      return this.agendaDetailsBtnString();
    },
    minicalHeader : function(a, f) {
      this.setAttributes(a, {
        id : f + "",
        "aria-live" : "assertice",
        "aria-atomic" : "true"
      });
    },
    minicalGrid : function(obj, fn) {
      this.setAttributes(obj, {
        "aria-labelledby" : fn + "",
        role : "grid"
      });
    },
    minicalRow : function(node) {
      this.setAttributes(node, {
        role : "row"
      });
    },
    minicalDayCell : function(size, date) {
      /** @type {boolean} */
      var selected = date.valueOf() < scheduler._max_date.valueOf() && date.valueOf() >= scheduler._min_date.valueOf();
      this.setAttributes(size, {
        role : "gridcell",
        "aria-label" : scheduler.templates.day_date(date),
        "aria-selected" : selected ? "true" : "false"
      });
    },
    minicalHeadCell : function(node) {
      this.setAttributes(node, {
        role : "columnheader"
      });
    },
    weekAgendaDayCell : function(objectNodeBox, attrName) {
      var maxExtent = objectNodeBox.querySelector(".dhx_wa_scale_bar");
      var root = objectNodeBox.querySelector(".dhx_wa_day_data");
      /** @type {string} */
      var id = scheduler.uid() + "";
      this.setAttributes(maxExtent, {
        id : id
      });
      this.setAttributes(root, {
        "aria-labelledby" : id
      });
    },
    weekAgendaEvent : function(colInfos, data) {
      this.eventAttr(data, colInfos);
    },
    lightboxHiddenAttr : function(label) {
      label.setAttribute("aria-hidden", "true");
    },
    lightboxVisibleAttr : function(childElement) {
      childElement.setAttribute("aria-hidden", "false");
    },
    lightboxSectionButtonAttrString : function(ariaLabel) {
      return this.getAttributeString({
        role : "button",
        "aria-label" : ariaLabel,
        tabindex : "0"
      });
    },
    yearHeader : function(size, section) {
      this.setAttributes(size, {
        id : section + ""
      });
    },
    yearGrid : function(e, skipFrames) {
      this.minicalGrid(e, skipFrames);
    },
    yearHeadCell : function(inmediate_node) {
      return this.minicalHeadCell(inmediate_node);
    },
    yearRow : function(inmediate_node) {
      return this.minicalRow(inmediate_node);
    },
    yearDayCell : function(a) {
      this.setAttributes(a, {
        role : "gridcell"
      });
    },
    lightboxAttr : function(element) {
      element.setAttribute("role", "dialog");
      element.setAttribute("aria-hidden", "true");
      element.firstChild.setAttribute("role", "heading");
    },
    lightboxButtonAttrString : function(button) {
      return this.getAttributeString({
        role : "button",
        "aria-label" : scheduler.locale.labels[button],
        tabindex : "0"
      });
    },
    eventMenuAttrString : function(button) {
      return this.getAttributeString({
        role : "button",
        "aria-label" : scheduler.locale.labels[button]
      });
    },
    lightboxHeader : function(t, f) {
      t.setAttribute("aria-label", f);
    },
    lightboxSelectAttrString : function(klass) {
      /** @type {string} */
      var interval = "";
      switch(klass) {
        case "%Y":
          interval = scheduler.locale.labels.year;
          break;
        case "%m":
          interval = scheduler.locale.labels.month;
          break;
        case "%d":
          interval = scheduler.locale.labels.day;
          break;
        case "%H:%i":
          /** @type {string} */
          interval = scheduler.locale.labels.hour + " " + scheduler.locale.labels.minute;
      }
      return scheduler._waiAria.getAttributeString({
        "aria-label" : interval
      });
    },
    messageButtonAttrString : function(a22) {
      return "tabindex='0' role='button' aria-label='" + a22 + "'";
    },
    messageInfoAttr : function(close) {
      close.setAttribute("role", "alert");
    },
    messageModalAttr : function(container, t1) {
      container.setAttribute("role", "dialog");
      if (t1) {
        container.setAttribute("aria-labelledby", t1);
      }
    },
    quickInfoAttr : function(box) {
      box.setAttribute("role", "dialog");
    },
    quickInfoHeaderAttrString : function() {
      return " role='heading' ";
    },
    quickInfoHeader : function(n, s) {
      n.setAttribute("aria-label", s);
    },
    quickInfoButtonAttrString : function(ariaLabel) {
      return scheduler._waiAria.getAttributeString({
        role : "button",
        "aria-label" : ariaLabel,
        tabindex : "0"
      });
    },
    tooltipAttr : function(elem) {
      elem.setAttribute("role", "tooltip");
    },
    tooltipVisibleAttr : function(childElement) {
      childElement.setAttribute("aria-hidden", "false");
    },
    tooltipHiddenAttr : function(ul) {
      ul.setAttribute("aria-hidden", "true");
    }
  };
  var name;
  for (name in scheduler._waiAria) {
    scheduler._waiAria[name] = function(CropAreaRectangle) {
      return function() {
        return listStarterkits() ? " " : CropAreaRectangle.apply(this, arguments);
      };
    }(scheduler._waiAria[name]);
  }
}(), dhtmlxEventable(scheduler), scheduler._detachDomEvent = function(el, sEvt, PFnc) {
  if (el.removeEventListener) {
    el.removeEventListener(sEvt, PFnc, false);
  } else {
    if (el.detachEvent) {
      el.detachEvent("on" + sEvt, PFnc);
    }
  }
}, scheduler._init_once = function() {
  /**
   * @param {!Element} a
   * @return {?}
   */
  function onclick(a) {
    /** @type {!HTMLBodyElement} */
    var b = document.body;
    for (; a && a != b;) {
      a = a.parentNode;
    }
    return !(b != a);
  }
  /**
   * @return {?}
   */
  function _getWindowSize() {
    return {
      w : window.innerWidth || document.documentElement.clientWidth,
      h : window.innerHeight || document.documentElement.clientHeight
    };
  }
  /**
   * @param {!Window} trimRect
   * @param {!Window} srcSize
   * @return {?}
   */
  function continue2_(trimRect, srcSize) {
    return trimRect.w == srcSize.w && trimRect.h == srcSize.h;
  }
  var roomName = _getWindowSize();
  dhtmlxEvent(window, "resize", function() {
    if (onclick(scheduler._obj)) {
      window.clearTimeout(scheduler._resize_timer);
      scheduler._resize_timer = window.setTimeout(function() {
        var test3 = _getWindowSize();
        if (!continue2_(roomName, test3)) {
          if (!onclick(scheduler._obj)) {
            return;
          }
          if (scheduler.callEvent("onSchedulerResize", [])) {
            scheduler.updateView();
            scheduler.callEvent("onAfterSchedulerResize", []);
          }
        }
        roomName = test3;
      }, 100);
    }
  });
  /**
   * @return {undefined}
   */
  scheduler._init_once = function() {
  };
}, scheduler.init = function(id, view, initial) {
  view = view || scheduler._currentDate();
  initial = initial || "week";
  if (this._obj) {
    this.unset_actions();
  }
  this._obj = "string" == typeof id ? document.getElementById(id) : id;
  this.$container = this._obj;
  if (this.config.wai_aria_attributes && this.config.wai_aria_application_role) {
    this.$container.setAttribute("role", "application");
  }
  if (this._skin_init) {
    scheduler._skin_init();
  }
  scheduler.date.init();
  /** @type {!Array} */
  this._els = [];
  /** @type {boolean} */
  this._scroll = true;
  this._quirks = _isIE && "BackCompat" == document.compatMode;
  this._quirks7 = _isIE && -1 == navigator.appVersion.indexOf("MSIE 8");
  this.get_elements();
  this.init_templates();
  this.set_actions();
  this._init_once();
  this._init_touch_events();
  this.set_sizes();
  scheduler.callEvent("onSchedulerReady", []);
  this.setCurrentView(view, initial);
}, scheduler.xy = {
  min_event_height : 40,
  scale_width : 50,
  scroll_width : 18,
  scale_height : 20,
  month_scale_height : 20,
  menu_width : 25,
  margin_top : 0,
  margin_left : 0,
  editor_width : 140,
  month_head_height : 22,
  event_header_height : 14
}, scheduler.keys = {
  edit_save : 13,
  edit_cancel : 27
}, scheduler.bind = function(object, fn) {
  return object.bind ? object.bind(fn) : function() {
    return object.apply(fn, arguments);
  };
}, scheduler.set_sizes = function() {
  /** @type {number} */
  var x = this._x = this._obj.clientWidth - this.xy.margin_left;
  /** @type {number} */
  var y = this._y = this._obj.clientHeight - this.xy.margin_top;
  var _nc_x = this._table_view ? 0 : this.xy.scale_width + this.xy.scroll_width;
  var xOnly = this._table_view ? -1 : this.xy.scale_width;
  var el = this.$container.querySelector(".dhx_cal_scale_placeholder");
  if (scheduler._is_material_skin()) {
    if (!el) {
      /** @type {!Element} */
      el = document.createElement("div");
      /** @type {string} */
      el.className = "dhx_cal_scale_placeholder";
      this.$container.insertBefore(el, this._els.dhx_cal_header[0]);
    }
    /** @type {string} */
    el.style.display = "block";
    this.set_xy(el, x, this.xy.scale_height + 1, 0, this.xy.nav_height + (this._quirks ? -1 : 1));
  } else {
    if (el) {
      el.parentNode.removeChild(el);
    }
  }
  this.set_xy(this._els.dhx_cal_navline[0], x, this.xy.nav_height, 0, 0);
  this.set_xy(this._els.dhx_cal_header[0], x - _nc_x, this.xy.scale_height, xOnly, this.xy.nav_height + (this._quirks ? -1 : 1));
  var windowheight = this._els.dhx_cal_navline[0].offsetHeight;
  if (windowheight > 0) {
    this.xy.nav_height = windowheight;
  }
  var popup_height = this.xy.scale_height + this.xy.nav_height + (this._quirks ? -2 : 0);
  this.set_xy(this._els.dhx_cal_data[0], x, y - (popup_height + 2), 0, popup_height + 2);
}, scheduler.set_xy = function(obj, i, width, x, a) {
  /** @type {string} */
  obj.style.width = Math.max(0, i) + "px";
  /** @type {string} */
  obj.style.height = Math.max(0, width) + "px";
  if (arguments.length > 3) {
    /** @type {string} */
    obj.style.left = x + "px";
    /** @type {string} */
    obj.style.top = a + "px";
  }
}, scheduler.get_elements = function() {
  var e = this._obj.getElementsByTagName("DIV");
  /** @type {number} */
  var i = 0;
  for (; i < e.length; i++) {
    var name = scheduler._getClassName(e[i]);
    var key = e[i].getAttribute("name") || "";
    if (name) {
      name = name.split(" ")[0];
    }
    if (!this._els[name]) {
      /** @type {!Array} */
      this._els[name] = [];
    }
    this._els[name].push(e[i]);
    var html = scheduler.locale.labels[key || name];
    if ("string" != typeof html && key && !e[i].innerHTML) {
      html = key.split("_")[0];
    }
    if (html) {
      this._waiAria.labelAttr(e[i], html);
      e[i].innerHTML = html;
    }
  }
}, scheduler.unset_actions = function() {
  var name;
  for (name in this._els) {
    if (this._click[name]) {
      /** @type {number} */
      var i = 0;
      for (; i < this._els[name].length; i++) {
        /** @type {null} */
        this._els[name][i].onclick = null;
      }
    }
  }
  /** @type {null} */
  this._obj.onselectstart = null;
  /** @type {null} */
  this._obj.onmousemove = null;
  /** @type {null} */
  this._obj.onmousedown = null;
  /** @type {null} */
  this._obj.onmouseup = null;
  /** @type {null} */
  this._obj.ondblclick = null;
  /** @type {null} */
  this._obj.oncontextmenu = null;
}, scheduler.set_actions = function() {
  var name;
  for (name in this._els) {
    if (this._click[name]) {
      /** @type {number} */
      var i = 0;
      for (; i < this._els[name].length; i++) {
        this._els[name][i].onclick = scheduler._click[name];
      }
    }
  }
  /**
   * @param {?} event
   * @return {?}
   */
  this._obj.onselectstart = function(event) {
    return false;
  };
  /**
   * @param {string} e
   * @return {undefined}
   */
  this._obj.onmousemove = function(e) {
    if (!scheduler._temp_touch_block) {
      scheduler._on_mouse_move(e || event);
    }
  };
  /**
   * @param {string} e
   * @return {undefined}
   */
  this._obj.onmousedown = function(e) {
    if (!scheduler._ignore_next_click) {
      scheduler._on_mouse_down(e || event);
    }
  };
  /**
   * @param {string} e
   * @return {undefined}
   */
  this._obj.onmouseup = function(e) {
    if (!scheduler._ignore_next_click) {
      scheduler._on_mouse_up(e || event);
    }
  };
  /**
   * @param {string} ev
   * @return {undefined}
   */
  this._obj.ondblclick = function(ev) {
    scheduler._on_dbl_click(ev || event);
  };
  /**
   * @param {string} e
   * @return {?}
   */
  this._obj.oncontextmenu = function(e) {
    var ev = e || event;
    var files = ev.target || ev.srcElement;
    var status = scheduler.callEvent("onContextMenu", [scheduler._locate_event(files), ev]);
    return status;
  };
}, scheduler.select = function(id) {
  if (this._select_id != id) {
    scheduler._close_not_saved();
    this.editStop(false);
    this.unselect();
    /** @type {string} */
    this._select_id = id;
    this.updateEvent(id);
  }
}, scheduler.unselect = function(selector) {
  if (!selector || selector == this._select_id) {
    var id = this._select_id;
    /** @type {null} */
    this._select_id = null;
    if (id && this.getEvent(id)) {
      this.updateEvent(id);
    }
  }
}, scheduler.getState = function() {
  return {
    mode : this._mode,
    date : new Date(this._date),
    min_date : new Date(this._min_date),
    max_date : new Date(this._max_date),
    editor_id : this._edit_id,
    lightbox_id : this._lightbox_id,
    new_event : this._new_event,
    select_id : this._select_id,
    expanded : this.expanded,
    drag_id : this._drag_id,
    drag_mode : this._drag_mode
  };
}, scheduler._click = {
  dhx_cal_data : function(e) {
    if (scheduler._ignore_next_click) {
      return e.preventDefault && e.preventDefault(), e.cancelBubble = true, scheduler._ignore_next_click = false, false;
    }
    var i = e ? e.target : event.srcElement;
    var id = scheduler._locate_event(i);
    if (e = e || event, id) {
      if (!scheduler.callEvent("onClick", [id, e]) || scheduler.config.readonly) {
        return;
      }
    } else {
      scheduler.callEvent("onEmptyClick", [scheduler.getActionData(e).date, e]);
    }
    if (id && scheduler.config.select) {
      scheduler.select(id);
      var mask = scheduler._getClassName(i);
      if (-1 != mask.indexOf("_icon")) {
        scheduler._click.buttons[mask.split(" ")[1].replace("icon_", "")](id);
      }
    } else {
      scheduler._close_not_saved();
      if ((new Date).valueOf() - (scheduler._new_event || 0) > 500) {
        scheduler.unselect();
      }
    }
  },
  dhx_cal_prev_button : function() {
    scheduler._click.dhx_cal_next_button(0, -1);
  },
  dhx_cal_next_button : function(index, time) {
    scheduler.setCurrentView(scheduler.date.add(scheduler.date[scheduler._mode + "_start"](new Date(scheduler._date)), time || 1, scheduler._mode));
  },
  dhx_cal_today_button : function() {
    if (scheduler.callEvent("onBeforeTodayDisplayed", [])) {
      scheduler.setCurrentView(scheduler._currentDate());
    }
  },
  dhx_cal_tab : function() {
    var field_name = this.getAttribute("name");
    var nm = field_name.substring(0, field_name.search("_tab"));
    scheduler.setCurrentView(scheduler._date, nm);
  },
  buttons : {
    "delete" : function(id) {
      var temp = scheduler.locale.labels.confirm_deleting;
      scheduler._dhtmlx_confirm(temp, scheduler.locale.labels.title_confirm_deleting, function() {
        scheduler.deleteEvent(id);
      });
    },
    edit : function(id) {
      scheduler.edit(id);
    },
    save : function(asNew) {
      scheduler.editStop(true);
    },
    details : function(e) {
      scheduler.showLightbox(e);
    },
    cancel : function(trackMechanism) {
      scheduler.editStop(false);
    }
  }
}, scheduler._dhtmlx_confirm = function(match, url, i) {
  if (!match) {
    return i();
  }
  var msg = {
    text : match
  };
  if (url) {
    /** @type {string} */
    msg.title = url;
  }
  if (i) {
    /**
     * @param {string} value
     * @return {undefined}
     */
    msg.callback = function(value) {
      if (value) {
        i();
      }
    };
  }
  dhtmlx.confirm(msg);
}, scheduler.addEventNow = function(data, val, state) {
  var params = {};
  if (scheduler._isObject(data) && !scheduler._isDate(data)) {
    /** @type {number} */
    params = data;
    /** @type {null} */
    data = null;
  }
  /** @type {number} */
  var step = 6e4 * (this.config.event_duration || this.config.time_step);
  if (!data) {
    data = params.start_date || Math.round(scheduler._currentDate().valueOf() / step) * step;
  }
  /** @type {!Date} */
  var first = new Date(data);
  if (!val) {
    var i = this.config.first_hour;
    if (i > first.getHours()) {
      first.setHours(i);
      /** @type {number} */
      data = first.valueOf();
    }
    val = data.valueOf() + step;
  }
  /** @type {!Date} */
  var d = new Date(val);
  if (first.valueOf() == d.valueOf()) {
    d.setTime(d.valueOf() + step);
  }
  params.start_date = params.start_date || first;
  params.end_date = params.end_date || d;
  params.text = params.text || this.locale.labels.new_event;
  params.id = this._drag_id = params.id || this.uid();
  /** @type {string} */
  this._drag_mode = "new-size";
  /** @type {boolean} */
  this._loading = true;
  var getInfoResponse = this.addEvent(params);
  return this.callEvent("onEventCreated", [this._drag_id, state]), this._loading = false, this._drag_event = {}, this._on_mouse_up(state), getInfoResponse;
}, scheduler._on_dbl_click = function(e, target) {
  if (target = target || e.target || e.srcElement, !this.config.readonly) {
    var i = scheduler._getClassName(target).split(" ")[0];
    switch(i) {
      case "dhx_scale_holder":
      case "dhx_scale_holder_now":
      case "dhx_month_body":
      case "dhx_wa_day_data":
        if (!scheduler.config.dblclick_create) {
          break;
        }
        this.addEventNow(this.getActionData(e).date, null, e);
        break;
      case "dhx_cal_event":
      case "dhx_wa_ev_body":
      case "dhx_agenda_line":
      case "dhx_grid_event":
      case "dhx_cal_event_line":
      case "dhx_cal_event_clear":
        var id = this._locate_event(target);
        if (!this.callEvent("onDblClick", [id, e])) {
          return;
        }
        if (this.config.details_on_dblclick || this._table_view || !this.getEvent(id)._timed || !this.config.select) {
          this.showLightbox(id);
        } else {
          this.edit(id);
        }
        break;
      case "dhx_time_block":
      case "dhx_cal_container":
        return;
      default:
        var onBodyKeyup = this["dblclick_" + i];
        if (onBodyKeyup) {
          onBodyKeyup.call(this, e);
        } else {
          if (target.parentNode && target != this) {
            return scheduler._on_dbl_click(e, target.parentNode);
          }
        }
    }
  }
}, scheduler._get_column_index = function(index) {
  /** @type {number} */
  var colIndex = 0;
  if (this._cols) {
    /** @type {number} */
    var left = 0;
    /** @type {number} */
    var i = 0;
    for (; left + this._cols[i] < index && i < this._cols.length;) {
      left = left + this._cols[i];
      i++;
    }
    if (colIndex = i + (this._cols[i] ? (index - left) / this._cols[i] : 0), this._ignores && colIndex >= this._cols.length) {
      for (; colIndex >= 1 && this._ignores[Math.floor(colIndex)];) {
        colIndex--;
      }
    }
  }
  return colIndex;
}, scheduler._week_indexes_from_pos = function(plainObject) {
  if (this._cols) {
    var arrowOffsetTop = this._get_column_index(plainObject.x);
    return plainObject.x = Math.min(this._cols.length - 1, Math.max(0, Math.ceil(arrowOffsetTop) - 1)), plainObject.y = Math.max(0, Math.ceil(60 * plainObject.y / (this.config.time_step * this.config.hour_size_px)) - 1) + this.config.first_hour * (60 / this.config.time_step), plainObject;
  }
  return plainObject;
}, scheduler._mouse_coords = function(ev) {
  var self;
  /** @type {!HTMLBodyElement} */
  var body = document.body;
  /** @type {!Element} */
  var documentElement = document.documentElement;
  /** @type {({x: ?, y: ?}|{x: number, y: number})} */
  self = _isIE || !ev.pageX && !ev.pageY ? {
    x : ev.clientX + (body.scrollLeft || documentElement.scrollLeft || 0) - body.clientLeft,
    y : ev.clientY + (body.scrollTop || documentElement.scrollTop || 0) - body.clientTop
  } : {
    x : ev.pageX,
    y : ev.pageY
  };
  self.x -= this.$domHelpers.getAbsoluteLeft(this._obj) + (this._table_view ? 0 : this.xy.scale_width);
  self.y -= this.$domHelpers.getAbsoluteTop(this._obj) + this.xy.nav_height + (this._dy_shift || 0) + this.xy.scale_height - this._els.dhx_cal_data[0].scrollTop;
  /** @type {!Event} */
  self.ev = ev;
  var callbackOnArrival = this["mouse_" + this._mode];
  if (callbackOnArrival) {
    self = callbackOnArrival.call(this, self);
  } else {
    if (this._table_view) {
      var topDelta = this._get_column_index(self.x);
      if (!this._cols || !this._colsS) {
        return self;
      }
      /** @type {number} */
      var i = 0;
      /** @type {number} */
      i = 1;
      for (; i < this._colsS.heights.length && !(this._colsS.heights[i] > self.y); i++) {
      }
      /** @type {number} */
      self.y = Math.ceil(24 * (Math.max(0, topDelta) + 7 * Math.max(0, i - 1)) * 60 / this.config.time_step);
      if (scheduler._drag_mode || "month" == this._mode) {
        /** @type {number} */
        self.y = 24 * (Math.max(0, Math.ceil(topDelta) - 1) + 7 * Math.max(0, i - 1)) * 60 / this.config.time_step;
      }
      if ("move" == this._drag_mode && scheduler._ignores_detected && scheduler.config.preserve_length) {
        /** @type {boolean} */
        self._ignores = true;
        if (!this._drag_event._event_length) {
          this._drag_event._event_length = this._get_real_event_length(this._drag_event.start_date, this._drag_event.end_date, {
            x_step : 1,
            x_unit : "day"
          });
        }
      }
      /** @type {number} */
      self.x = 0;
    } else {
      self = this._week_indexes_from_pos(self);
    }
  }
  return self.timestamp = +new Date, self;
}, scheduler._close_not_saved = function() {
  if ((new Date).valueOf() - (scheduler._new_event || 0) > 500 && scheduler._edit_id) {
    var temp = scheduler.locale.labels.confirm_closing;
    scheduler._dhtmlx_confirm(temp, scheduler.locale.labels.title_confirm_closing, function() {
      scheduler.editStop(scheduler.config.positive_closing);
    });
    if (temp) {
      /** @type {null} */
      this._drag_id = this._drag_pos = this._drag_mode = null;
    }
  }
}, scheduler._correct_shift = function(t, isTangent) {
  return t = t - 6e4 * ((new Date(scheduler._min_date)).getTimezoneOffset() - (new Date(t)).getTimezoneOffset()) * (isTangent ? -1 : 1);
}, scheduler._is_pos_changed = function(e, data) {
  /**
   * @param {(boolean|number|string)} s
   * @param {(boolean|number|string)} e
   * @param {number} value
   * @return {?}
   */
  function touchEnd(s, e, value) {
    return !!(Math.abs(s - e) > value);
  }
  if (!e || !this._drag_pos) {
    return true;
  }
  /** @type {number} */
  var r = 100;
  /** @type {number} */
  var clientY = 5;
  return !!(this._drag_pos.has_moved || !this._drag_pos.timestamp || data.timestamp - this._drag_pos.timestamp > r || touchEnd(e.ev.clientX, data.ev.clientX, clientY) || touchEnd(e.ev.clientY, data.ev.clientY, clientY));
}, scheduler._correct_drag_start_date = function(start) {
  var event;
  if (scheduler.matrix) {
    event = scheduler.matrix[scheduler._mode];
  }
  event = event || {
    x_step : 1,
    x_unit : "day"
  };
  /** @type {!Date} */
  start = new Date(start);
  /** @type {number} */
  var interval = 1;
  return (event._start_correction || event._end_correction) && (interval = 60 * (event.last_hour || 0) - (60 * start.getHours() + start.getMinutes()) || 1), 1 * start + (scheduler._get_fictional_event_length(start, interval, event) - interval);
}, scheduler._correct_drag_end_date = function(name, context) {
  var event;
  if (scheduler.matrix) {
    event = scheduler.matrix[scheduler._mode];
  }
  event = event || {
    x_step : 1,
    x_unit : "day"
  };
  var url = 1 * name + scheduler._get_fictional_event_length(name, context, event);
  return new Date(1 * url - (scheduler._get_fictional_event_length(url, -1, event, -1) + 1));
}, scheduler._on_mouse_move = function(event) {
  if (this._drag_mode) {
    var pos = this._mouse_coords(event);
    if (this._is_pos_changed(this._drag_pos, pos)) {
      var start;
      var date;
      if (this._edit_id != this._drag_id && this._close_not_saved(), !this._drag_mode) {
        return;
      }
      /** @type {null} */
      var next = null;
      if (this._drag_pos && !this._drag_pos.has_moved && (next = this._drag_pos, next.has_moved = true), this._drag_pos = pos, this._drag_pos.has_moved = true, "create" == this._drag_mode) {
        if (next && (pos = next), this._close_not_saved(), this.unselect(this._select_id), this._loading = true, start = this._get_date_from_pos(pos).valueOf(), !this._drag_start) {
          var result = this.callEvent("onBeforeEventCreated", [event, this._drag_id]);
          return result ? (this._loading = false, void(this._drag_start = start)) : void(this._loading = false);
        }
        date = start;
        date == this._drag_start;
        /** @type {!Date} */
        var input = new Date(this._drag_start);
        /** @type {!Date} */
        var f = new Date(date);
        if (!("day" != this._mode && "week" != this._mode || input.getHours() != f.getHours() || input.getMinutes() != f.getMinutes())) {
          /** @type {!Date} */
          f = new Date(this._drag_start + 1e3);
        }
        this._drag_id = this.uid();
        this.addEvent(input, f, this.locale.labels.new_event, this._drag_id, pos.fields);
        this.callEvent("onEventCreated", [this._drag_id, event]);
        /** @type {boolean} */
        this._loading = false;
        /** @type {string} */
        this._drag_mode = "new-size";
      }
      var obj;
      var ev = this.getEvent(this._drag_id);
      if (scheduler.matrix && (obj = scheduler.matrix[scheduler._mode]), obj = obj || {
        x_step : 1,
        x_unit : "day"
      }, "move" == this._drag_mode) {
        start = this._min_date.valueOf() + 6e4 * (pos.y * this.config.time_step + 24 * pos.x * 60 - (scheduler._move_pos_shift || 0));
        if (!pos.custom && this._table_view) {
          start = start + 1e3 * this.date.time_part(ev.start_date);
        }
        start = this._correct_shift(start);
        if (pos._ignores && this.config.preserve_length && this._table_view) {
          start = scheduler._correct_drag_start_date(start);
          date = scheduler._correct_drag_end_date(start, this._drag_event._event_length);
        } else {
          /** @type {number} */
          date = ev.end_date.valueOf() - (ev.start_date.valueOf() - start);
        }
      } else {
        if (start = ev.start_date.valueOf(), date = ev.end_date.valueOf(), this._table_view) {
          var d = this._min_date.valueOf() + pos.y * this.config.time_step * 6e4 + (pos.custom ? 0 : 864e5);
          if ("month" == this._mode) {
            if (d = this._correct_shift(d, false), this._drag_from_start) {
              /** @type {number} */
              var end = 864e5;
              if (d <= scheduler.date.date_part(new Date(date + end - 1)).valueOf()) {
                /** @type {number} */
                start = d - end;
              }
            } else {
              date = d;
            }
          } else {
            if (this.config.preserve_length) {
              if (pos.resize_from_start) {
                start = scheduler._correct_drag_start_date(d);
              } else {
                date = scheduler._correct_drag_end_date(d, 0);
              }
            } else {
              if (pos.resize_from_start) {
                start = d;
              } else {
                date = d;
              }
            }
          }
        } else {
          var elapsed = this.date.date_part(new Date(ev.end_date.valueOf() - 1)).valueOf();
          /** @type {!Date} */
          var dCurrent = new Date(elapsed);
          date = elapsed + pos.y * this.config.time_step * 6e4;
          date = date + 6e4 * ((new Date(date)).getTimezoneOffset() - dCurrent.getTimezoneOffset());
          /** @type {string} */
          this._els.dhx_cal_data[0].style.cursor = "s-resize";
          if ("week" == this._mode || "day" == this._mode) {
            date = this._correct_shift(date);
          }
        }
        if ("new-size" == this._drag_mode) {
          if (date <= this._drag_start) {
            var params = pos.shift || (this._table_view && !pos.custom ? 864e5 : 0);
            /** @type {number} */
            start = date - (pos.shift ? 0 : params);
            date = this._drag_start + (params || 6e4 * this.config.time_step);
          } else {
            start = this._drag_start;
          }
        } else {
          if (start >= date) {
            date = start + 6e4 * this.config.time_step;
          }
        }
      }
      /** @type {!Date} */
      var before = new Date(date - 1);
      /** @type {!Date} */
      var d = new Date(start);
      if ("move" == this._drag_mode && scheduler.config.limit_drag_out && (+d < +scheduler._min_date || +date > +scheduler._max_date)) {
        if (+ev.start_date < +scheduler._min_date || +ev.end_date > +scheduler._max_date) {
          /** @type {!Date} */
          d = new Date(ev.start_date);
          /** @type {!Date} */
          date = new Date(ev.end_date);
        } else {
          /** @type {number} */
          var diff = date - d;
          if (+d < +scheduler._min_date) {
            /** @type {!Date} */
            d = new Date(scheduler._min_date);
            if (pos._ignores && this.config.preserve_length && this._table_view) {
              /** @type {!Date} */
              d = new Date(scheduler._correct_drag_start_date(d));
              if (obj._start_correction) {
                /** @type {!Date} */
                d = new Date(d.valueOf() + obj._start_correction);
              }
              /** @type {!Date} */
              date = new Date(1 * d + this._get_fictional_event_length(d, this._drag_event._event_length, obj));
            } else {
              /** @type {!Date} */
              date = new Date(+d + diff);
            }
          } else {
            /** @type {!Date} */
            date = new Date(scheduler._max_date);
            if (pos._ignores && this.config.preserve_length && this._table_view) {
              if (obj._end_correction) {
                /** @type {!Date} */
                date = new Date(date.valueOf() - obj._end_correction);
              }
              /** @type {!Date} */
              date = new Date(1 * date - this._get_fictional_event_length(date, 0, obj, true));
              /** @type {!Date} */
              d = new Date(1 * date - this._get_fictional_event_length(date, this._drag_event._event_length, obj, true));
              if (this._ignores_detected) {
                d = scheduler.date.add(d, obj.x_step, obj.x_unit);
                /** @type {!Date} */
                date = new Date(1 * date - this._get_fictional_event_length(date, 0, obj, true));
                date = scheduler.date.add(date, obj.x_step, obj.x_unit);
              }
            } else {
              /** @type {!Date} */
              d = new Date(+date - diff);
            }
          }
        }
        /** @type {!Date} */
        before = new Date(date - 1);
      }
      if (!this._table_view && !scheduler.config.all_timed && (!scheduler._get_section_view() && pos.x != this._get_event_sday({
        start_date : new Date(date),
        end_date : new Date(date)
      }) || (new Date(date)).getHours() >= this.config.last_hour)) {
        /** @type {number} */
        diff = date - d;
        end = this._min_date.valueOf() + 24 * pos.x * 60 * 6e4;
        date = scheduler.date.date_part(new Date(end));
        date.setHours(this.config.last_hour);
        /** @type {!Date} */
        before = new Date(date - 1);
        if ("move" == this._drag_mode) {
          /** @type {!Date} */
          d = new Date(+date - diff);
        }
      }
      if (this._table_view || before.getDate() == d.getDate() && before.getHours() < this.config.last_hour || scheduler._allow_dnd) {
        if (ev.start_date = d, ev.end_date = new Date(date), this.config.update_render) {
          var contentScrollTop = scheduler._els.dhx_cal_data[0].scrollTop;
          this.update_view();
          scheduler._els.dhx_cal_data[0].scrollTop = contentScrollTop;
        } else {
          this.updateEvent(this._drag_id);
        }
      }
      if (this._table_view) {
        this.for_rendered(this._drag_id, function(_doodle) {
          _doodle.className += " dhx_in_move dhx_cal_event_drag";
        });
      }
      this.callEvent("onEventDrag", [this._drag_id, this._drag_mode, event]);
    }
  } else {
    if (scheduler.checkEvent("onMouseMove")) {
      var id = this._locate_event(event.target || event.srcElement);
      this.callEvent("onMouseMove", [id, event]);
    }
  }
}, scheduler._on_mouse_down = function(e, target) {
  if (2 != e.button && !this.config.readonly && !this._drag_mode) {
    target = target || e.target || e.srcElement;
    var id = scheduler._getClassName(target).split(" ")[0];
    switch(id) {
      case "dhx_cal_event_line":
      case "dhx_cal_event_clear":
        if (this._table_view) {
          /** @type {string} */
          this._drag_mode = "move";
        }
        break;
      case "dhx_event_move":
      case "dhx_wa_ev_body":
        /** @type {string} */
        this._drag_mode = "move";
        break;
      case "dhx_event_resize":
        /** @type {string} */
        this._drag_mode = "resize";
        var targetVariants = scheduler._getClassName(target);
        if (targetVariants.indexOf("dhx_event_resize_end") < 0) {
          /** @type {boolean} */
          scheduler._drag_from_start = true;
        } else {
          /** @type {boolean} */
          scheduler._drag_from_start = false;
        }
        break;
      case "dhx_scale_holder":
      case "dhx_scale_holder_now":
      case "dhx_month_body":
      case "dhx_matrix_cell":
      case "dhx_marked_timespan":
        /** @type {string} */
        this._drag_mode = "create";
        break;
      case "":
        if (target.parentNode) {
          return scheduler._on_mouse_down(e, target.parentNode);
        }
        break;
      default:
        if ((!scheduler.checkEvent("onMouseDown") || scheduler.callEvent("onMouseDown", [id, e])) && target.parentNode && target != this && "dhx_body" != id) {
          return scheduler._on_mouse_down(e, target.parentNode);
        }
        /** @type {null} */
        this._drag_mode = null;
        /** @type {null} */
        this._drag_id = null;
    }
    if (this._drag_mode) {
      var group = this._locate_event(target);
      if (this.config["drag_" + this._drag_mode] && this.callEvent("onBeforeDrag", [group, this._drag_mode, e])) {
        if (this._drag_id = group, (this._edit_id != this._drag_id || this._edit_id && "create" == this._drag_mode) && this._close_not_saved(), !this._drag_mode) {
          return;
        }
        this._drag_event = scheduler._lame_clone(this.getEvent(this._drag_id) || {});
        this._drag_pos = this._mouse_coords(e);
      } else {
        /** @type {number} */
        this._drag_mode = this._drag_id = 0;
      }
    }
    /** @type {null} */
    this._drag_start = null;
  }
}, scheduler._get_private_properties = function(array) {
  var conf_shortcuts_icon = {};
  var i;
  for (i in array) {
    if (0 === i.indexOf("_")) {
      /** @type {boolean} */
      conf_shortcuts_icon[i] = true;
    }
  }
  return conf_shortcuts_icon;
}, scheduler._clear_temporary_properties = function(ss, what) {
  var internal = this._get_private_properties(ss);
  var cost = this._get_private_properties(what);
  var k;
  for (k in cost) {
    if (!internal[k]) {
      delete what[k];
    }
  }
}, scheduler._on_mouse_up = function(event) {
  if (!event || 2 != event.button || !this._mobile) {
    if (this._drag_mode && this._drag_id) {
      /** @type {string} */
      this._els.dhx_cal_data[0].style.cursor = "default";
      var id = this._drag_id;
      var dhtmlObject = this._drag_mode;
      var r = !this._drag_pos || this._drag_pos.has_moved;
      var ev = this.getEvent(this._drag_id);
      if (r && (this._drag_event._dhx_changed || !this._drag_event.start_date || ev.start_date.valueOf() != this._drag_event.start_date.valueOf() || ev.end_date.valueOf() != this._drag_event.end_date.valueOf())) {
        /** @type {boolean} */
        var domask = "new-size" == this._drag_mode;
        if (this.callEvent("onBeforeEventChanged", [ev, event, domask, this._drag_event])) {
          if (this._drag_id = this._drag_mode = null, domask && this.config.edit_on_create) {
            if (this.unselect(), this._new_event = new Date, this._table_view || this.config.details_on_create || !this.config.select || !this.isOneDayEvent(this.getEvent(id))) {
              return scheduler.callEvent("onDragEnd", [id, dhtmlObject, event]), this.showLightbox(id);
            }
            /** @type {boolean} */
            this._drag_pos = true;
            this._select_id = this._edit_id = id;
          } else {
            if (!this._new_event) {
              this.callEvent(domask ? "onEventAdded" : "onEventChanged", [id, this.getEvent(id)]);
            }
          }
        } else {
          if (domask) {
            this.deleteEvent(ev.id, true);
          } else {
            /** @type {boolean} */
            this._drag_event._dhx_changed = false;
            this._clear_temporary_properties(ev, this._drag_event);
            scheduler._lame_copy(ev, this._drag_event);
            this.updateEvent(ev.id);
          }
        }
      }
      if (this._drag_pos && (this._drag_pos.has_moved || this._drag_pos === true)) {
        /** @type {null} */
        this._drag_id = this._drag_mode = null;
        this.render_view_data();
      }
      scheduler.callEvent("onDragEnd", [id, dhtmlObject, event]);
    }
    /** @type {null} */
    this._drag_id = null;
    /** @type {null} */
    this._drag_mode = null;
    /** @type {null} */
    this._drag_pos = null;
  }
}, scheduler._trigger_dyn_loading = function() {
  return this._load_mode && this._load() ? (this._render_wait = true, true) : false;
}, scheduler.update_view = function() {
  this._reset_ignores();
  var best_of = this[this._mode + "_view"];
  return best_of ? best_of(true) : this._reset_scale(), this._trigger_dyn_loading() ? true : void this.render_view_data();
}, scheduler.isViewExists = function(name) {
  return !!(scheduler[name + "_view"] || scheduler.date[name + "_start"] && scheduler.templates[name + "_date"] && scheduler.templates[name + "_scale_date"]);
}, scheduler._set_aria_buttons_attrs = function() {
  /** @type {!Array} */
  var m = ["dhx_cal_next_button", "dhx_cal_prev_button", "dhx_cal_tab", "dhx_cal_today_button"];
  /** @type {number} */
  var k = 0;
  for (; k < m.length; k++) {
    var resources = this._els[m[k]];
    /** @type {number} */
    var i = 0;
    for (; resources && i < resources.length; i++) {
      var name = resources[i].getAttribute("name");
      var context = this.locale.labels[m[k]];
      if (name) {
        context = this.locale.labels[name] || context;
      }
      if ("dhx_cal_next_button" == m[k]) {
        context = this.locale.labels.next;
      } else {
        if ("dhx_cal_prev_button" == m[k]) {
          context = this.locale.labels.prev;
        }
      }
      this._waiAria.headerButtonsAttributes(resources[i], context || "");
    }
  }
}, scheduler.updateView = function(type, mode) {
  type = type || this._date;
  mode = mode || this._mode;
  /** @type {string} */
  var i = "dhx_cal_data";
  var settings = this._obj;
  /** @type {string} */
  var record = "dhx_scheduler_" + this._mode;
  /** @type {string} */
  var value = "dhx_scheduler_" + mode;
  if (this._mode && -1 != settings.className.indexOf(record)) {
    settings.className = settings.className.replace(record, value);
  } else {
    settings.className += " " + value;
  }
  var height;
  /** @type {string} */
  var name = "dhx_multi_day";
  var end = this._mode == mode && this.config.preserve_scroll ? this._els[i][0].scrollTop : false;
  if (this._els[name] && this._els[name][0]) {
    height = this._els[name][0].scrollTop;
  }
  if (this[this._mode + "_view"] && mode && this._mode != mode) {
    this[this._mode + "_view"](false);
  }
  this._close_not_saved();
  if (this._els[name]) {
    this._els[name][0].parentNode.removeChild(this._els[name][0]);
    /** @type {null} */
    this._els[name] = null;
  }
  /** @type {string} */
  this._mode = mode;
  /** @type {!Object} */
  this._date = type;
  /** @type {boolean} */
  this._table_view = "month" == this._mode;
  /** @type {number} */
  this._dy_shift = 0;
  this._set_aria_buttons_attrs();
  var locationArray = this._els.dhx_cal_tab;
  if (locationArray) {
    /** @type {number} */
    var j = 0;
    for (; j < locationArray.length; j++) {
      var cell = locationArray[j];
      var cs = cell.className;
      cs = cs.replace(/ active/g, "");
      if (cell.getAttribute("name") == this._mode + "_tab") {
        /** @type {string} */
        cs = cs + " active";
        this._waiAria.headerToggleState(cell, true);
      } else {
        this._waiAria.headerToggleState(cell, false);
      }
      cell.className = cs;
    }
  }
  this.update_view();
  if ("number" == typeof end) {
    /** @type {number} */
    this._els[i][0].scrollTop = end;
  }
  if ("number" == typeof height && this._els[name] && this._els[name][0]) {
    /** @type {number} */
    this._els[name][0].scrollTop = height;
  }
}, scheduler.setCurrentView = function(view, a) {
  if (this.callEvent("onBeforeViewChange", [this._mode, this._date, a || this._mode, view || this._date])) {
    this.updateView(view, a);
    this.callEvent("onViewChange", [this._mode, this._date]);
  }
}, scheduler._render_x_header = function(name, t, n, c, close) {
  close = close || 0;
  /** @type {!Element} */
  var m = document.createElement("div");
  /** @type {string} */
  m.className = "dhx_scale_bar";
  if (this.templates[this._mode + "_scalex_class"]) {
    m.className += " " + this.templates[this._mode + "_scalex_class"](n);
  }
  /** @type {number} */
  var startStrat = this._cols[name] - 1;
  if ("month" == this._mode && 0 === name && this.config.left_border) {
    m.className += " dhx_scale_bar_border";
    t = t + 1;
  }
  this.set_xy(m, startStrat, this.xy.scale_height - 2, t, close);
  var e = this.templates[this._mode + "_scale_date"](n, this._mode);
  m.innerHTML = e;
  this._waiAria.dayHeaderAttr(m, e);
  c.appendChild(m);
}, scheduler._get_columns_num = function(array, key) {
  /** @type {number} */
  var i = 7;
  if (!scheduler._table_view) {
    var nearMedian = scheduler.date["get_" + scheduler._mode + "_end"];
    if (nearMedian) {
      key = nearMedian(array);
    }
    /** @type {number} */
    i = Math.round((key.valueOf() - array.valueOf()) / 864e5);
  }
  return i;
}, scheduler._get_timeunit_start = function() {
  return this.date[this._mode + "_start"](new Date(this._date.valueOf()));
}, scheduler._get_view_end = function() {
  var val = this._get_timeunit_start();
  var msg = scheduler.date.add(val, 1, this._mode);
  if (!scheduler._table_view) {
    var sprintf = scheduler.date["get_" + scheduler._mode + "_end"];
    if (sprintf) {
      msg = sprintf(val);
    }
  }
  return msg;
}, scheduler._calc_scale_sizes = function(animate, data, count) {
  /** @type {number} */
  var summ = animate;
  var val = this._get_columns_num(data, count);
  this._process_ignores(data, val, "day", 1);
  /** @type {number} */
  var sub = val - this._ignores_detected;
  /** @type {number} */
  var i = 0;
  for (; val > i; i++) {
    if (this._ignores[i]) {
      /** @type {number} */
      this._cols[i] = 0;
      sub++;
    } else {
      /** @type {number} */
      this._cols[i] = Math.floor(summ / (sub - i));
    }
    /** @type {number} */
    summ = summ - this._cols[i];
    this._colsS[i] = (this._cols[i - 1] || 0) + (this._colsS[i - 1] || (this._table_view ? 0 : this.xy.scale_width + 2));
  }
  this._colsS.col_length = val;
  this._colsS[val] = this._cols[val - 1] + this._colsS[val - 1] || 0;
}, scheduler._set_scale_col_size = function(nodeInfo, callback, coords) {
  var config = this.config;
  this.set_xy(nodeInfo, callback - 1, config.hour_size_px * (config.last_hour - config.first_hour), coords + this.xy.scale_width + 1, 0);
}, scheduler._render_scales = function(e, t) {
  /** @type {!Date} */
  var output = new Date(scheduler._min_date);
  /** @type {!Date} */
  var min = new Date(scheduler._max_date);
  var val = this.date.date_part(scheduler._currentDate());
  /** @type {number} */
  var newPosition = parseInt(e.style.width, 10);
  /** @type {!Date} */
  var date = new Date(this._min_date);
  var diff = this._get_columns_num(output, min);
  this._calc_scale_sizes(newPosition, output, min);
  /** @type {number} */
  var left = 0;
  /** @type {string} */
  e.innerHTML = "";
  /** @type {number} */
  var i = 0;
  for (; diff > i; i++) {
    if (this._ignores[i] || this._render_x_header(i, left, date, e), !this._table_view) {
      /** @type {!Element} */
      var row = document.createElement("div");
      /** @type {string} */
      var key = "dhx_scale_holder";
      if (date.valueOf() == val.valueOf()) {
        /** @type {string} */
        key = "dhx_scale_holder_now";
      }
      if (this._ignores_detected && this._ignores[i]) {
        /** @type {string} */
        key = key + " dhx_scale_ignore";
      }
      row.className = key + " " + this.templates.week_date_class(date, val);
      this._waiAria.dayColumnAttr(row, date);
      this._set_scale_col_size(row, this._cols[i], left);
      t.appendChild(row);
      this.callEvent("onScaleAdd", [row, date]);
    }
    left = left + this._cols[i];
    date = this.date.add(date, 1, "day");
    date = this.date.day_start(date);
  }
}, scheduler._reset_scale = function() {
  if (this.templates[this._mode + "_date"]) {
    var e = this._els.dhx_cal_header[0];
    var d = this._els.dhx_cal_data[0];
    var c = this.config;
    /** @type {string} */
    e.innerHTML = "";
    /** @type {string} */
    d.innerHTML = "";
    /** @type {string} */
    var i = (c.readonly || !c.drag_resize ? " dhx_resize_denied" : "") + (c.readonly || !c.drag_move ? " dhx_move_denied" : "");
    /** @type {string} */
    d.className = "dhx_cal_data" + i;
    this._scales = {};
    /** @type {!Array} */
    this._cols = [];
    this._colsS = {
      height : 0
    };
    /** @type {number} */
    this._dy_shift = 0;
    this.set_sizes();
    var temp4;
    var dd;
    var sd = this._get_timeunit_start();
    var elem = scheduler._get_view_end();
    temp4 = dd = this._table_view ? scheduler.date.week_start(sd) : sd;
    this._min_date = temp4;
    var msg = this.templates[this._mode + "_date"](sd, elem, this._mode);
    if (this._els.dhx_cal_date[0].innerHTML = msg, this._waiAria.navBarDateAttr(this._els.dhx_cal_date[0], msg), this._max_date = elem, scheduler._render_scales(e, d), this._table_view) {
      this._reset_month_scale(d, sd, dd);
    } else {
      if (this._reset_hours_scale(d, sd, dd), c.multi_day) {
        /** @type {string} */
        var name = "dhx_multi_day";
        if (this._els[name]) {
          this._els[name][0].parentNode.removeChild(this._els[name][0]);
          /** @type {null} */
          this._els[name] = null;
        }
        var aTargetElement = this._els.dhx_cal_navline[0];
        var messageRegExp = aTargetElement.offsetHeight + this._els.dhx_cal_header[0].offsetHeight + 1;
        /** @type {!Element} */
        var e = document.createElement("div");
        /** @type {string} */
        e.className = name;
        /** @type {string} */
        e.style.visibility = "hidden";
        this.set_xy(e, Math.max(this._colsS[this._colsS.col_length] + this.xy.scroll_width - 2, 0), 0, 0, messageRegExp);
        d.parentNode.insertBefore(e, d);
        /** @type {!Element} */
        var label = e.cloneNode(true);
        /** @type {string} */
        label.className = name + "_icon";
        /** @type {string} */
        label.style.visibility = "hidden";
        this.set_xy(label, this.xy.scale_width, 0, 0, messageRegExp);
        e.appendChild(label);
        /** @type {!Array} */
        this._els[name] = [e, label];
        this._els[name][0].onclick = this._click.dhx_cal_data;
      }
    }
  }
}, scheduler._reset_hours_scale = function(e, value, type) {
  /** @type {!Element} */
  var r = document.createElement("div");
  /** @type {string} */
  r.className = "dhx_scale_holder";
  /** @type {!Date} */
  var d = new Date(1980, 1, 1, this.config.first_hour, 0, 0);
  /** @type {number} */
  var i = 1 * this.config.first_hour;
  for (; i < this.config.last_hour; i++) {
    /** @type {!Element} */
    var content = document.createElement("div");
    /** @type {string} */
    content.className = "dhx_scale_hour";
    /** @type {string} */
    content.style.height = this.config.hour_size_px + "px";
    var bg_w = this.xy.scale_width;
    if (this.config.left_border) {
      content.className += " dhx_scale_hour_border";
    }
    /** @type {string} */
    content.style.width = bg_w + "px";
    var type = scheduler.templates.hour_scale(d);
    content.innerHTML = type;
    this._waiAria.hourScaleAttr(content, type);
    r.appendChild(content);
    d = this.date.add(d, 1, "hour");
  }
  e.appendChild(r);
  if (this.config.scroll_hour) {
    /** @type {number} */
    e.scrollTop = this.config.hour_size_px * (this.config.scroll_hour - this.config.first_hour);
  }
}, scheduler._currentDate = function() {
  return scheduler.config.now_date ? new Date(scheduler.config.now_date) : new Date;
}, scheduler._reset_ignores = function() {
  this._ignores = {};
  /** @type {number} */
  this._ignores_detected = 0;
}, scheduler._process_ignores = function(obj, val, name, r, agumentsArr) {
  this._reset_ignores();
  var handler = scheduler["ignore_" + this._mode];
  if (handler) {
    /** @type {!Date} */
    var x = new Date(obj);
    /** @type {number} */
    var i = 0;
    for (; val > i; i++) {
      if (handler(x)) {
        this._ignores_detected += 1;
        /** @type {boolean} */
        this._ignores[i] = true;
        if (agumentsArr) {
          val++;
        }
      }
      x = scheduler.date.add(x, r, name);
      if (scheduler.date[name + "_start"]) {
        x = scheduler.date[name + "_start"](x);
      }
    }
  }
}, scheduler._render_month_scale = function(x, t, value, length) {
  /**
   * @param {number} i
   * @return {?}
   */
  function format(i) {
    var upperHeight = scheduler._colsS.height;
    return void 0 !== scheduler._colsS.heights[i + 1] && (upperHeight = scheduler._colsS.heights[i + 1] - (scheduler._colsS.heights[i] || 0)), upperHeight;
  }
  var date = scheduler.date.add(t, 1, "month");
  /** @type {!Date} */
  var temp4 = new Date(value);
  var now = scheduler._currentDate();
  this.date.date_part(now);
  this.date.date_part(value);
  length = length || Math.ceil(Math.round((date.valueOf() - value.valueOf()) / 864e5) / 7);
  /** @type {!Array} */
  var result = [];
  /** @type {number} */
  var i = 0;
  for (; 7 >= i; i++) {
    /** @type {number} */
    var v = (this._cols[i] || 0) - 1;
    if (0 === i && this.config.left_border) {
      /** @type {number} */
      v = v - 1;
    }
    /** @type {string} */
    result[i] = v + "px";
  }
  /** @type {number} */
  var s = 0;
  /** @type {!Element} */
  var inShadowTable = document.createElement("table");
  inShadowTable.setAttribute("cellpadding", "0");
  inShadowTable.setAttribute("cellspacing", "0");
  /** @type {!Element} */
  var inShadowTbody = document.createElement("tbody");
  inShadowTable.appendChild(inShadowTbody);
  /** @type {!Array} */
  var stack = [];
  /** @type {number} */
  i = 0;
  for (; length > i; i++) {
    /** @type {!Element} */
    var inRow1 = document.createElement("tr");
    inShadowTbody.appendChild(inRow1);
    /** @type {number} */
    var bg_h = Math.max(format(i) - scheduler.xy.month_head_height, 0);
    /** @type {number} */
    var j = 0;
    for (; 7 > j; j++) {
      /** @type {!Element} */
      var body = document.createElement("td");
      inRow1.appendChild(body);
      /** @type {string} */
      var rgb = "";
      if (t > value) {
        /** @type {string} */
        rgb = "dhx_before";
      } else {
        if (value >= date) {
          /** @type {string} */
          rgb = "dhx_after";
        } else {
          if (value.valueOf() == now.valueOf()) {
            /** @type {string} */
            rgb = "dhx_now";
          }
        }
      }
      if (this._ignores_detected && this._ignores[j]) {
        /** @type {string} */
        rgb = rgb + " dhx_scale_ignore";
      }
      body.className = rgb + " " + this.templates.month_date_class(value, now);
      /** @type {string} */
      var yi = "dhx_month_body";
      /** @type {string} */
      var y = "dhx_month_head";
      if (0 === j && this.config.left_border && (yi = yi + " dhx_month_body_border", y = y + " dhx_month_head_border"), this._ignores_detected && this._ignores[j]) {
        body.appendChild(document.createElement("div"));
        body.appendChild(document.createElement("div"));
      } else {
        this._waiAria.monthCellAttr(body, value);
        /** @type {!Element} */
        var data = document.createElement("div");
        /** @type {string} */
        data.className = y;
        data.innerHTML = this.templates.month_day(value);
        body.appendChild(data);
        /** @type {!Element} */
        var ret = document.createElement("div");
        /** @type {string} */
        ret.className = yi;
        /** @type {string} */
        ret.style.height = bg_h + "px";
        ret.style.width = result[j];
        body.appendChild(ret);
      }
      stack.push(value);
      var i = value.getDate();
      value = this.date.add(value, 1, "day");
      if (value.getDate() - i > 1) {
        /** @type {!Date} */
        value = new Date(value.getFullYear(), value.getMonth(), i + 1, 12, 0);
      }
    }
    scheduler._colsS.heights[i] = s;
    s = s + format(i);
  }
  /** @type {!Date} */
  this._min_date = temp4;
  /** @type {!Object} */
  this._max_date = value;
  /** @type {string} */
  x.innerHTML = "";
  x.appendChild(inShadowTable);
  this._scales = {};
  var symbol = x.getElementsByTagName("div");
  /** @type {number} */
  i = 0;
  for (; i < stack.length; i++) {
    x = symbol[2 * i + 1];
    var state = stack[i];
    /** @type {!Object} */
    this._scales[+state] = x;
  }
  /** @type {number} */
  i = 0;
  for (; i < stack.length; i++) {
    state = stack[i];
    this.callEvent("onScaleAdd", [this._scales[+state], state]);
  }
  return this._max_date;
}, scheduler._reset_month_scale = function(e, d, value, h) {
  var date = scheduler.date.add(d, 1, "month");
  var now = scheduler._currentDate();
  this.date.date_part(now);
  this.date.date_part(value);
  h = h || Math.ceil(Math.round((date.valueOf() - value.valueOf()) / 864e5) / 7);
  /** @type {number} */
  var _viewPortH = Math.floor(e.clientHeight / h) - this.xy.month_head_height;
  return this._colsS.height = _viewPortH + this.xy.month_head_height, this._colsS.heights = [], scheduler._render_month_scale(e, d, value, h);
}, scheduler.getLabel = function(feature, id) {
  var settings = this.config.lightbox.sections;
  /** @type {number} */
  var j = 0;
  for (; j < settings.length; j++) {
    if (settings[j].map_to == feature) {
      var entries = settings[j].options;
      /** @type {number} */
      var i = 0;
      for (; i < entries.length; i++) {
        if (entries[i].key == id) {
          return entries[i].label;
        }
      }
    }
  }
  return "";
}, scheduler.updateCollection = function(pos, values) {
  var p = scheduler.serverList(pos);
  return p ? (p.splice(0, p.length), p.push.apply(p, values || []), scheduler.callEvent("onOptionsLoad", []), scheduler.resetLightbox(), true) : false;
}, scheduler._lame_clone = function(data, key) {
  var i;
  var _ref;
  var c;
  key = key || [];
  /** @type {number} */
  i = 0;
  for (; i < key.length; i = i + 2) {
    if (data === key[i]) {
      return key[i + 1];
    }
  }
  if (data && "object" == typeof data) {
    c = {};
    /** @type {!Array} */
    _ref = [Array, Date, Number, String, Boolean];
    /** @type {number} */
    i = 0;
    for (; i < _ref.length; i++) {
      if (data instanceof _ref[i]) {
        c = i ? new _ref[i](data) : new _ref[i];
      }
    }
    key.push(data, c);
    for (i in data) {
      if (Object.prototype.hasOwnProperty.apply(data, [i])) {
        c[i] = scheduler._lame_clone(data[i], key);
      }
    }
  }
  return c || data;
}, scheduler._lame_copy = function(el, h) {
  var i;
  for (i in h) {
    if (h.hasOwnProperty(i)) {
      el[i] = h[i];
    }
  }
  return el;
}, scheduler._get_date_from_pos = function(pos) {
  var day = this._min_date.valueOf() + 6e4 * (pos.y * this.config.time_step + 24 * (this._table_view ? 0 : pos.x) * 60);
  return new Date(this._correct_shift(day));
}, scheduler.getActionData = function(value) {
  var i = this._mouse_coords(value);
  return {
    date : this._get_date_from_pos(i),
    section : i.section
  };
}, scheduler._focus = function(item, element) {
  if (item && item.focus) {
    if (this._mobile) {
      window.setTimeout(function() {
        item.focus();
      }, 10);
    } else {
      try {
        if (element && item.select && item.offsetWidth) {
          item.select();
        }
        item.focus();
      } catch (i) {
      }
    }
  }
}, scheduler._get_real_event_length = function(c, t, obj) {
  var pos;
  /** @type {number} */
  var regExBonusMultiplier = t - c;
  var CommentMatchPenalty = obj._start_correction + obj._end_correction || 0;
  var f = this["ignore_" + this._mode];
  /** @type {number} */
  var found = 0;
  if (obj.render) {
    found = this._get_date_index(obj, c);
    pos = this._get_date_index(obj, t);
  } else {
    /** @type {number} */
    pos = Math.round(regExBonusMultiplier / 60 / 60 / 1e3 / 24);
  }
  /** @type {boolean} */
  var l = true;
  for (; pos > found;) {
    var r = scheduler.date.add(t, -obj.x_step, obj.x_unit);
    if (f && f(t) && (!l || l && f(r))) {
      /** @type {number} */
      regExBonusMultiplier = regExBonusMultiplier - (t - r);
    } else {
      /** @type {boolean} */
      l = false;
      /** @type {number} */
      regExBonusMultiplier = regExBonusMultiplier - CommentMatchPenalty;
    }
    t = r;
    pos--;
  }
  return regExBonusMultiplier;
}, scheduler._get_fictional_event_length = function(str, i, obj, isNegative) {
  /** @type {!Date} */
  var s = new Date(str);
  /** @type {number} */
  var dir = isNegative ? -1 : 1;
  if (obj._start_correction || obj._end_correction) {
    var y;
    /** @type {number} */
    y = isNegative ? 60 * s.getHours() + s.getMinutes() - 60 * (obj.first_hour || 0) : 60 * (obj.last_hour || 0) - (60 * s.getHours() + s.getMinutes());
    /** @type {number} */
    var scale = 60 * (obj.last_hour - obj.first_hour);
    /** @type {number} */
    var fullScaleHeight = Math.ceil((i / 6e4 - y) / scale);
    if (0 > fullScaleHeight) {
      /** @type {number} */
      fullScaleHeight = 0;
    }
    i = i + fullScaleHeight * (1440 - scale) * 60 * 1e3;
  }
  var pos;
  /** @type {!Date} */
  var start = new Date(1 * str + i * dir);
  var isDijit = this["ignore_" + this._mode];
  /** @type {number} */
  var offset = 0;
  if (obj.render) {
    offset = this._get_date_index(obj, s);
    pos = this._get_date_index(obj, start);
  } else {
    /** @type {number} */
    pos = Math.round(i / 60 / 60 / 1e3 / 24);
  }
  for (; pos * dir >= offset * dir;) {
    var e = scheduler.date.add(s, obj.x_step * dir, obj.x_unit);
    if (isDijit && isDijit(s)) {
      i = i + (e - s) * dir;
      /** @type {number} */
      pos = pos + dir;
    }
    s = e;
    /** @type {number} */
    offset = offset + dir;
  }
  return i;
}, scheduler._get_section_view = function() {
  return this.matrix && this.matrix[this._mode] ? this.matrix[this._mode] : this._props && this._props[this._mode] ? this._props[this._mode] : null;
}, scheduler._get_section_property = function() {
  return this.matrix && this.matrix[this._mode] ? this.matrix[this._mode].y_property : this._props && this._props[this._mode] ? this._props[this._mode].map_to : null;
}, scheduler._is_initialized = function() {
  var curr = this.getState();
  return this._obj && curr.date && curr.mode;
}, scheduler._is_lightbox_open = function() {
  var store = this.getState();
  return null !== store.lightbox_id && void 0 !== store.lightbox_id;
}, scheduler._getClassName = function(el) {
  if (!el) {
    return "";
  }
  var className = el.className || "";
  return className.baseVal && (className = className.baseVal), className.indexOf || (className = ""), className || "";
}, scheduler.$domHelpers = {
  getAbsoluteLeft : function(node) {
    return this.getOffset(node).left;
  },
  getAbsoluteTop : function(node) {
    return this.getOffset(node).top;
  },
  getOffsetSum : function(elem) {
    /** @type {number} */
    var b = 0;
    /** @type {number} */
    var indicatorLeft = 0;
    for (; elem;) {
      /** @type {number} */
      b = b + parseInt(elem.offsetTop);
      /** @type {number} */
      indicatorLeft = indicatorLeft + parseInt(elem.offsetLeft);
      elem = elem.offsetParent;
    }
    return {
      top : b,
      left : indicatorLeft
    };
  },
  getOffsetRect : function(element) {
    var b = element.getBoundingClientRect();
    /** @type {number} */
    var i = 0;
    /** @type {number} */
    var left = 0;
    if (/Mobi/.test(navigator.userAgent)) {
      /** @type {!Element} */
      var c = document.createElement("div");
      /** @type {string} */
      c.style.position = "absolute";
      /** @type {string} */
      c.style.left = "0px";
      /** @type {string} */
      c.style.top = "0px";
      /** @type {string} */
      c.style.width = "1px";
      /** @type {string} */
      c.style.height = "1px";
      document.body.appendChild(c);
      /** @type {!ClientRect} */
      var s = c.getBoundingClientRect();
      /** @type {number} */
      i = b.top - s.top;
      /** @type {number} */
      left = b.left - s.left;
      c.parentNode.removeChild(c);
    } else {
      /** @type {!HTMLBodyElement} */
      var body = document.body;
      /** @type {!Element} */
      var docElem = document.documentElement;
      /** @type {number} */
      var buttonHeight = window.pageYOffset || docElem.scrollTop || body.scrollTop;
      /** @type {number} */
      var x = window.pageXOffset || docElem.scrollLeft || body.scrollLeft;
      /** @type {number} */
      var centerLineMargin = docElem.clientTop || body.clientTop || 0;
      /** @type {number} */
      var dx = docElem.clientLeft || body.clientLeft || 0;
      /** @type {number} */
      i = b.top + buttonHeight - centerLineMargin;
      /** @type {number} */
      left = b.left + x - dx;
    }
    return {
      top : Math.round(i),
      left : Math.round(left)
    };
  },
  getOffset : function(element) {
    return element.getBoundingClientRect ? this.getOffsetRect(element) : this.getOffsetSum(element);
  }
}, scheduler.$env = {
  isIE : navigator.userAgent.indexOf("MSIE") >= 0 || navigator.userAgent.indexOf("Trident") >= 0,
  isIE6 : !window.XMLHttpRequest && navigator.userAgent.indexOf("MSIE") >= 0,
  isIE7 : navigator.userAgent.indexOf("MSIE 7.0") >= 0 && navigator.userAgent.indexOf("Trident") < 0,
  isIE8 : navigator.userAgent.indexOf("MSIE 8.0") >= 0 && navigator.userAgent.indexOf("Trident") >= 0,
  isOpera : navigator.userAgent.indexOf("Opera") >= 0,
  isChrome : navigator.userAgent.indexOf("Chrome") >= 0,
  isKHTML : navigator.userAgent.indexOf("Safari") >= 0 || navigator.userAgent.indexOf("Konqueror") >= 0,
  isFF : navigator.userAgent.indexOf("Firefox") >= 0,
  isIPad : navigator.userAgent.search(/iPad/gi) >= 0,
  isEdge : -1 != navigator.userAgent.indexOf("Edge")
}, scheduler.$ajax = {
  _obj : scheduler,
  cache : true,
  method : "get",
  parse : function(string) {
    if ("string" != typeof string) {
      return string;
    }
    var xmlDoc;
    return string = string.replace(/^[\s]+/, ""), window.DOMParser && !scheduler.$env.isIE ? xmlDoc = (new window.DOMParser).parseFromString(string, "text/xml") : window.ActiveXObject !== window.undefined && (xmlDoc = new window.ActiveXObject("Microsoft.XMLDOM"), xmlDoc.async = "false", xmlDoc.loadXML(string)), xmlDoc;
  },
  xmltop : function(items, response, isApi) {
    if ("undefined" == typeof response.status || response.status < 400) {
      var doc = response.responseXML ? response.responseXML || response : this.parse(response.responseText || response);
      if (doc && null !== doc.documentElement && !doc.getElementsByTagName("parsererror").length) {
        return doc.getElementsByTagName(items)[0];
      }
    }
    return -1 !== isApi && this._obj.callEvent("onLoadXMLError", ["Incorrect XML", arguments[1], isApi]), document.createElement("DIV");
  },
  xpath : function(node, doc) {
    if (doc.nodeName || (doc = doc.responseXML || doc), scheduler.$env.isIE) {
      return doc.selectNodes(node) || [];
    }
    var varg;
    /** @type {!Array} */
    var results = [];
    var elements = (doc.ownerDocument || doc).evaluate(node, doc, null, XPathResult.ANY_TYPE, null);
    for (;;) {
      if (varg = elements.iterateNext(), !varg) {
        break;
      }
      results.push(varg);
    }
    return results;
  },
  query : function(config) {
    this._call(config.method || "GET", config.url, config.data || "", config.async || true, config.callback, null, config.headers);
  },
  get : function(obj, params) {
    this._call("GET", obj, null, true, params);
  },
  getSync : function(obj) {
    return this._call("GET", obj, null, false);
  },
  put : function(key, callback, params) {
    this._call("PUT", key, callback, true, params);
  },
  del : function(key, callback, params) {
    this._call("DELETE", key, callback, true, params);
  },
  post : function(obj, method, params) {
    if (1 == arguments.length) {
      /** @type {string} */
      method = "";
    } else {
      if (2 != arguments.length || "function" != typeof method && "function" != typeof window[method]) {
        /** @type {string} */
        method = String(method);
      } else {
        /** @type {string} */
        params = method;
        /** @type {string} */
        method = "";
      }
    }
    this._call("POST", obj, method, true, params);
  },
  postSync : function(url, type) {
    return type = null === type ? "" : String(type), this._call("POST", url, type, false);
  },
  getLong : function(key, params) {
    this._call("GET", key, null, true, params, {
      url : key
    });
  },
  postLong : function(config, obj, params) {
    if (2 == arguments.length) {
      /** @type {!Object} */
      params = obj;
      /** @type {string} */
      obj = "";
    }
    this._call("POST", config, obj, true, params, {
      url : config,
      postData : obj
    });
  },
  _call : function(method, url, type, e, cb, data, headers) {
    var actual = this._obj;
    var t = window.XMLHttpRequest && !actual.$env.isIE ? new XMLHttpRequest : new ActiveXObject("Microsoft.XMLHTTP");
    /** @type {boolean} */
    var l = null !== navigator.userAgent.match(/AppleWebKit/) && null !== navigator.userAgent.match(/Qt/) && null !== navigator.userAgent.match(/Safari/);
    if (e && (t.onreadystatechange = function() {
      if (4 == t.readyState || l && 3 == t.readyState) {
        if ((200 != t.status || "" === t.responseText) && !actual.callEvent("onAjaxError", [t])) {
          return;
        }
        window.setTimeout(function() {
          if ("function" == typeof cb) {
            cb.apply(window, [{
              xmlDoc : t,
              filePath : url
            }]);
          }
          if (data) {
            if ("undefined" != typeof data.postData) {
              this.postLong(data.url, data.postData, cb);
            } else {
              this.getLong(data.url, cb);
            }
          }
          /** @type {null} */
          cb = null;
          /** @type {null} */
          t = null;
        }, 1);
      }
    }), "GET" != method || this.cache || (url = url + ((url.indexOf("?") >= 0 ? "&" : "?") + "dhxr" + (new Date).getTime() + "=1")), t.open(method, url, e), headers) {
      var i;
      for (i in headers) {
        t.setRequestHeader(i, headers[i]);
      }
    } else {
      if ("POST" == method.toUpperCase() || "PUT" == method || "DELETE" == method) {
        t.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");
      } else {
        if ("GET" == method) {
          /** @type {null} */
          type = null;
        }
      }
    }
    return t.setRequestHeader("X-Requested-With", "XMLHttpRequest"), t.send(type), e ? void 0 : {
      xmlDoc : t,
      filePath : url
    };
  },
  urlSeparator : function(unixPath) {
    return -1 != unixPath.indexOf("?") ? "&" : "?";
  }
}, scheduler.date = {
  init : function() {
    var rowsNames = scheduler.locale.date.month_short;
    var col = scheduler.locale.date.month_short_hash = {};
    /** @type {number} */
    var i = 0;
    for (; i < rowsNames.length; i++) {
      /** @type {number} */
      col[rowsNames[i]] = i;
    }
    rowsNames = scheduler.locale.date.month_full;
    col = scheduler.locale.date.month_full_hash = {};
    /** @type {number} */
    i = 0;
    for (; i < rowsNames.length; i++) {
      /** @type {number} */
      col[rowsNames[i]] = i;
    }
  },
  date_part : function(date) {
    /** @type {!Date} */
    var fulldate = new Date(date);
    return date.setHours(0), date.setMinutes(0), date.setSeconds(0), date.setMilliseconds(0), date.getHours() && (date.getDate() < fulldate.getDate() || date.getMonth() < fulldate.getMonth() || date.getFullYear() < fulldate.getFullYear()) && date.setTime(date.getTime() + 36e5 * (24 - date.getHours())), date;
  },
  time_part : function(a) {
    return (a.valueOf() / 1e3 - 60 * a.getTimezoneOffset()) % 86400;
  },
  week_start : function(d) {
    var t = d.getDay();
    return scheduler.config.start_on_monday && (0 === t ? t = 6 : t--), this.date_part(this.add(d, -1 * t, "day"));
  },
  month_start : function(newSelectedDate) {
    return newSelectedDate.setDate(1), this.date_part(newSelectedDate);
  },
  year_start : function(givenTime) {
    return givenTime.setMonth(0), this.month_start(givenTime);
  },
  day_start : function(date_string) {
    return this.date_part(date_string);
  },
  _add_days : function(d, v) {
    /** @type {!Date} */
    var self = new Date(d.valueOf());
    if (self.setDate(self.getDate() + v), v == Math.round(v) && v > 0) {
      /** @type {number} */
      var seconds = +self - +d;
      /** @type {number} */
      var s = seconds % 864e5;
      if (s && d.getTimezoneOffset() == self.getTimezoneOffset()) {
        /** @type {number} */
        var v1 = s / 36e5;
        self.setTime(self.getTime() + 60 * (24 - v1) * 60 * 1e3);
      }
    }
    return v >= 0 && !d.getHours() && self.getHours() && (self.getDate() < d.getDate() || self.getMonth() < d.getMonth() || self.getFullYear() < d.getFullYear()) && self.setTime(self.getTime() + 36e5 * (24 - self.getHours())), self;
  },
  add : function(date, i, value) {
    /** @type {!Date} */
    var t = new Date(date.valueOf());
    switch(value) {
      case "day":
        t = scheduler.date._add_days(t, i);
        break;
      case "week":
        t = scheduler.date._add_days(t, 7 * i);
        break;
      case "month":
        t.setMonth(t.getMonth() + i);
        break;
      case "year":
        t.setYear(t.getFullYear() + i);
        break;
      case "hour":
        t.setTime(t.getTime() + 60 * i * 60 * 1e3);
        break;
      case "minute":
        t.setTime(t.getTime() + 60 * i * 1e3);
        break;
      default:
        return scheduler.date["add_" + value](date, i, value);
    }
    return t;
  },
  to_fixed : function(e) {
    return 10 > e ? "0" + e : e;
  },
  copy : function(e) {
    return new Date(e.valueOf());
  },
  date_to_str : function(n, processPercent) {
    return n = n.replace(/%[a-zA-Z]/g, function(canCreateDiscussions) {
      switch(canCreateDiscussions) {
        case "%d":
          return '"+scheduler.date.to_fixed(date.getDate())+"';
        case "%m":
          return '"+scheduler.date.to_fixed((date.getMonth()+1))+"';
        case "%j":
          return '"+date.getDate()+"';
        case "%n":
          return '"+(date.getMonth()+1)+"';
        case "%y":
          return '"+scheduler.date.to_fixed(date.getFullYear()%100)+"';
        case "%Y":
          return '"+date.getFullYear()+"';
        case "%D":
          return '"+scheduler.locale.date.day_short[date.getDay()]+"';
        case "%l":
          return '"+scheduler.locale.date.day_full[date.getDay()]+"';
        case "%M":
          return '"+scheduler.locale.date.month_short[date.getMonth()]+"';
        case "%F":
          return '"+scheduler.locale.date.month_full[date.getMonth()]+"';
        case "%h":
          return '"+scheduler.date.to_fixed((date.getHours()+11)%12+1)+"';
        case "%g":
          return '"+((date.getHours()+11)%12+1)+"';
        case "%G":
          return '"+date.getHours()+"';
        case "%H":
          return '"+scheduler.date.to_fixed(date.getHours())+"';
        case "%i":
          return '"+scheduler.date.to_fixed(date.getMinutes())+"';
        case "%a":
          return '"+(date.getHours()>11?"pm":"am")+"';
        case "%A":
          return '"+(date.getHours()>11?"PM":"AM")+"';
        case "%s":
          return '"+scheduler.date.to_fixed(date.getSeconds())+"';
        case "%W":
          return '"+scheduler.date.to_fixed(scheduler.date.getISOWeek(date))+"';
        default:
          return canCreateDiscussions;
      }
    }), processPercent && (n = n.replace(/date\.get/g, "date.getUTC")), new Function("date", 'return "' + n + '";');
  },
  str_to_date : function(format, utc) {
    /** @type {string} */
    var currentColumn = "var temp=date.match(/[a-zA-Z]+|[0-9]+/g);";
    var crossfilterable_layers = format.match(/%[a-zA-Z]/g);
    /** @type {number} */
    var layer_i = 0;
    for (; layer_i < crossfilterable_layers.length; layer_i++) {
      switch(crossfilterable_layers[layer_i]) {
        case "%j":
        case "%d":
          /** @type {string} */
          currentColumn = currentColumn + ("set[2]=temp[" + layer_i + "]||1;");
          break;
        case "%n":
        case "%m":
          /** @type {string} */
          currentColumn = currentColumn + ("set[1]=(temp[" + layer_i + "]||1)-1;");
          break;
        case "%y":
          /** @type {string} */
          currentColumn = currentColumn + ("set[0]=temp[" + layer_i + "]*1+(temp[" + layer_i + "]>50?1900:2000);");
          break;
        case "%g":
        case "%G":
        case "%h":
        case "%H":
          /** @type {string} */
          currentColumn = currentColumn + ("set[3]=temp[" + layer_i + "]||0;");
          break;
        case "%i":
          /** @type {string} */
          currentColumn = currentColumn + ("set[4]=temp[" + layer_i + "]||0;");
          break;
        case "%Y":
          /** @type {string} */
          currentColumn = currentColumn + ("set[0]=temp[" + layer_i + "]||0;");
          break;
        case "%a":
        case "%A":
          /** @type {string} */
          currentColumn = currentColumn + ("set[3]=set[3]%12+((temp[" + layer_i + "]||'').toLowerCase()=='am'?0:12);");
          break;
        case "%s":
          /** @type {string} */
          currentColumn = currentColumn + ("set[5]=temp[" + layer_i + "]||0;");
          break;
        case "%M":
          /** @type {string} */
          currentColumn = currentColumn + ("set[1]=scheduler.locale.date.month_short_hash[temp[" + layer_i + "]]||0;");
          break;
        case "%F":
          /** @type {string} */
          currentColumn = currentColumn + ("set[1]=scheduler.locale.date.month_full_hash[temp[" + layer_i + "]]||0;");
      }
    }
    /** @type {string} */
    var id = "set[0],set[1],set[2],set[3],set[4],set[5]";
    return utc && (id = " Date.UTC(" + id + ")"), new Function("date", "var set=[0,0,1,0,0,0]; " + currentColumn + " return new Date(" + id + ");");
  },
  getISOWeek : function(date) {
    if (!date) {
      return false;
    }
    date = this.date_part(new Date(date));
    var t = date.getDay();
    if (0 === t) {
      /** @type {number} */
      t = 7;
    }
    /** @type {!Date} */
    var playdate = new Date(date.valueOf());
    playdate.setDate(date.getDate() + (4 - t));
    /** @type {number} */
    var stopDateString = playdate.getFullYear();
    /** @type {number} */
    var candidatesWidth = Math.round((playdate.getTime() - (new Date(stopDateString, 0, 1)).getTime()) / 864e5);
    /** @type {number} */
    var a = 1 + Math.floor(candidatesWidth / 7);
    return a;
  },
  getUTCISOWeek : function(searchDefinition) {
    return this.getISOWeek(this.convert_to_utc(searchDefinition));
  },
  convert_to_utc : function(d) {
    return new Date(d.getUTCFullYear(), d.getUTCMonth(), d.getUTCDate(), d.getUTCHours(), d.getUTCMinutes(), d.getUTCSeconds());
  }
}, scheduler.locale = {
  date : {
    month_full : ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"],
    month_short : ["Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"],
    day_full : ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"],
    day_short : ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"]
  },
  labels : {
    dhx_cal_today_button : "Today",
    day_tab : "Day",
    week_tab : "Week",
    month_tab : "Month",
    new_event : "New event",
    icon_save : "Save",
    icon_cancel : "Cancel",
    icon_details : "Details",
    icon_edit : "Edit",
    icon_delete : "Delete",
    confirm_closing : "",
    confirm_deleting : "Event will be deleted permanently, are you sure?",
    section_description : "Description",
    section_time : "Time period",
    full_day : "Full day",
    confirm_recurring : "Do you want to edit the whole set of repeated events?",
    section_recurring : "Repeat event",
    button_recurring : "Disabled",
    button_recurring_open : "Enabled",
    button_edit_series : "Edit series",
    button_edit_occurrence : "Edit occurrence",
    agenda_tab : "Agenda",
    date : "Date",
    description : "Description",
    year_tab : "Year",
    week_agenda_tab : "Agenda",
    grid_tab : "Grid",
    drag_to_create : "Drag to create",
    drag_to_move : "Drag to move",
    message_ok : "OK",
    message_cancel : "Cancel",
    next : "Next",
    prev : "Previous",
    year : "Year",
    month : "Month",
    day : "Day",
    hour : "Hour",
    minute : "Minute"
  }
}, scheduler.config = {
  default_date : "%j %M %Y",
  month_date : "%F %Y",
  load_date : "%Y-%m-%d",
  week_date : "%l",
  day_date : "%D, %F %j",
  hour_date : "%H:%i",
  month_day : "%d",
  xml_date : "%m/%d/%Y %H:%i",
  api_date : "%d-%m-%Y %H:%i",
  preserve_length : true,
  time_step : 5,
  start_on_monday : 1,
  first_hour : 0,
  last_hour : 24,
  readonly : false,
  drag_resize : 1,
  drag_move : 1,
  drag_create : 1,
  dblclick_create : 1,
  edit_on_create : 1,
  details_on_create : 0,
  resize_month_events : false,
  resize_month_timed : false,
  cascade_event_display : false,
  cascade_event_count : 4,
  cascade_event_margin : 30,
  multi_day : true,
  multi_day_height_limit : 0,
  drag_lightbox : true,
  preserve_scroll : true,
  select : true,
  server_utc : false,
  touch : true,
  touch_tip : true,
  touch_drag : 500,
  quick_info_detached : true,
  positive_closing : false,
  drag_highlight : true,
  limit_drag_out : false,
  icons_edit : ["icon_save", "icon_cancel"],
  icons_select : ["icon_details", "icon_edit", "icon_delete"],
  buttons_left : ["dhx_save_btn", "dhx_cancel_btn"],
  buttons_right : ["dhx_delete_btn"],
  lightbox : {
    sections : [{
      name : "description",
      map_to : "text",
      type : "textarea",
      focus : true
    }, {
      name : "time",
      height : 72,
      type : "time",
      map_to : "auto"
    }]
  },
  highlight_displayed_event : true,
  left_border : false,
  ajax_error : "alert",
  delay_render : 0,
  timeline_swap_resize : true,
  wai_aria_attributes : true,
  wai_aria_application_role : true
}, scheduler.config.buttons_left.$inital = scheduler.config.buttons_left.join(), scheduler.config.buttons_right.$inital = scheduler.config.buttons_right.join(), scheduler.templates = {}, scheduler.init_templates = function() {
  var styles = scheduler.locale.labels;
  styles.dhx_save_btn = styles.icon_save;
  styles.dhx_cancel_btn = styles.icon_cancel;
  styles.dhx_delete_btn = styles.icon_delete;
  var d = scheduler.date.date_to_str;
  var old = scheduler.config;
  /**
   * @param {!Object} options
   * @param {!Object} blob
   * @return {undefined}
   */
  var thisFor = function(options, blob) {
    var attr;
    for (attr in blob) {
      if (!options[attr]) {
        options[attr] = blob[attr];
      }
    }
  };
  thisFor(scheduler.templates, {
    day_date : d(old.default_date),
    month_date : d(old.month_date),
    week_date : function(end, date) {
      return scheduler.templates.day_date(end) + " &ndash; " + scheduler.templates.day_date(scheduler.date.add(date, -1, "day"));
    },
    day_scale_date : d(old.default_date),
    month_scale_date : d(old.week_date),
    week_scale_date : d(old.day_date),
    hour_scale : d(old.hour_date),
    time_picker : d(old.hour_date),
    event_date : d(old.hour_date),
    month_day : d(old.month_day),
    xml_date : scheduler.date.str_to_date(old.xml_date, old.server_utc),
    load_format : d(old.load_date),
    xml_format : d(old.xml_date, old.server_utc),
    api_date : scheduler.date.str_to_date(old.api_date),
    event_header : function(speed, start, handler) {
      return scheduler.templates.event_date(speed) + " - " + scheduler.templates.event_date(start);
    },
    event_text : function(cover_photo_to_crop, coords, selector) {
      return selector.text;
    },
    event_class : function(s, e, ev) {
      return "";
    },
    month_date_class : function(exprCode) {
      return "";
    },
    week_date_class : function(datetimestamp) {
      return "";
    },
    event_bar_date : function(start, end, ev) {
      return scheduler.templates.event_date(start) + " ";
    },
    event_bar_text : function(p, from, to) {
      return to.text;
    },
    month_events_link : function(error, filePath) {
      return "<a>View more(" + filePath + " events)</a>";
    },
    drag_marker_class : function(formatters, initialValue, type) {
      return "";
    },
    drag_marker_content : function(formatters, initialValue, type) {
      return "";
    },
    tooltip_date_format : scheduler.date.date_to_str("%Y-%m-%d %H:%i"),
    tooltip_text : function(start, end, event) {
      return "<b>Event:</b> " + event.text + "<br/><b>Start date:</b> " + scheduler.templates.tooltip_date_format(start) + "<br/><b>End date:</b> " + scheduler.templates.tooltip_date_format(end);
    }
  });
  this.callEvent("onTemplatesReady", []);
}, scheduler.uid = function() {
  return this._seed || (this._seed = (new Date).valueOf()), this._seed++;
}, scheduler._events = {}, scheduler.clearAll = function() {
  this._events = {};
  this._loaded = {};
  /** @type {null} */
  this._edit_id = null;
  /** @type {null} */
  this._select_id = null;
  /** @type {null} */
  this._drag_id = null;
  /** @type {null} */
  this._drag_mode = null;
  /** @type {null} */
  this._drag_pos = null;
  this.clear_view();
  this.callEvent("onClearAll", []);
}, scheduler.addEvent = function(obj, n, elem, location, args) {
  if (!arguments.length) {
    return this.addEventNow();
  }
  /** @type {string} */
  var data = obj;
  if (1 != arguments.length) {
    data = args || {};
    /** @type {string} */
    data.start_date = obj;
    /** @type {string} */
    data.end_date = n;
    /** @type {string} */
    data.text = elem;
    /** @type {string} */
    data.id = location;
  }
  data.id = data.id || scheduler.uid();
  data.text = data.text || "";
  if ("string" == typeof data.start_date) {
    data.start_date = this.templates.api_date(data.start_date);
  }
  if ("string" == typeof data.end_date) {
    data.end_date = this.templates.api_date(data.end_date);
  }
  /** @type {number} */
  var offset = 6e4 * (this.config.event_duration || this.config.time_step);
  if (data.start_date.valueOf() == data.end_date.valueOf()) {
    data.end_date.setTime(data.end_date.valueOf() + offset);
  }
  data._timed = this.isOneDayEvent(data);
  /** @type {boolean} */
  var d = !this._events[data.id];
  return this._events[data.id] = data, this.event_updated(data), this._loading || this.callEvent(d ? "onEventAdded" : "onEventChanged", [data.id, data]), data.id;
}, scheduler.deleteEvent = function(id, index) {
  var fn = this._events[id];
  if (index || this.callEvent("onBeforeEventDelete", [id, fn]) && this.callEvent("onConfirmedBeforeEventDelete", [id, fn])) {
    if (fn) {
      /** @type {null} */
      this._select_id = null;
      delete this._events[id];
      this.event_updated(fn);
      if (this._drag_id == fn.id) {
        /** @type {null} */
        this._drag_id = null;
        /** @type {null} */
        this._drag_mode = null;
        /** @type {null} */
        this._drag_pos = null;
      }
    }
    this.callEvent("onEventDeleted", [id, fn]);
  }
}, scheduler.getEvent = function(type) {
  return this._events[type];
}, scheduler.setEvent = function(type, event) {
  if (!event.id) {
    /** @type {string} */
    event.id = type;
  }
  /** @type {!Object} */
  this._events[type] = event;
}, scheduler.for_rendered = function(event_id, callback) {
  /** @type {number} */
  var i = this._rendered.length - 1;
  for (; i >= 0; i--) {
    if (this._rendered[i].getAttribute("event_id") == event_id) {
      callback(this._rendered[i], i);
    }
  }
}, scheduler.changeEventId = function(id, type) {
  if (id != type) {
    var event = this._events[id];
    if (event) {
      /** @type {string} */
      event.id = type;
      this._events[type] = event;
      delete this._events[id];
    }
    this.for_rendered(id, function(table) {
      table.setAttribute("event_id", type);
    });
    if (this._select_id == id) {
      /** @type {string} */
      this._select_id = type;
    }
    if (this._edit_id == id) {
      /** @type {string} */
      this._edit_id = type;
    }
    this.callEvent("onEventIdChange", [id, type]);
  }
}, function() {
  /** @type {!Array} */
  var args = ["text", "Text", "start_date", "StartDate", "end_date", "EndDate"];
  /**
   * @param {?} action
   * @return {?}
   */
  var getQuerier = function(action) {
    return function(key) {
      return scheduler.getEvent(key)[action];
    };
  };
  /**
   * @param {?} p
   * @return {?}
   */
  var renderPage = function(p) {
    return function(key, result) {
      var item = scheduler.getEvent(key);
      item[p] = result;
      /** @type {boolean} */
      item._changed = true;
      item._timed = this.isOneDayEvent(item);
      scheduler.event_updated(item, true);
    };
  };
  /** @type {number} */
  var i = 0;
  for (; i < args.length; i = i + 2) {
    scheduler["getEvent" + args[i + 1]] = getQuerier(args[i]);
    scheduler["setEvent" + args[i + 1]] = renderPage(args[i]);
  }
}(), scheduler.event_updated = function(obj, signatureOnly) {
  if (this.is_visible_events(obj)) {
    this.render_view_data();
  } else {
    this.clear_event(obj.id);
  }
}, scheduler.is_visible_events = function(event) {
  /** @type {boolean} */
  var t = event.start_date.valueOf() < this._max_date.valueOf() && this._min_date.valueOf() < event.end_date.valueOf();
  if (t) {
    var a = event.start_date.getHours();
    var r = event.end_date.getHours() + event.end_date.getMinutes() / 60;
    var c = this.config.last_hour;
    var b = this.config.first_hour;
    var n = this._table_view || !((r > c || b > r) && (a >= c || b > a));
    if (n) {
      return true;
    }
    /** @type {number} */
    var d = (event.end_date.valueOf() - event.start_date.valueOf()) / 36e5;
    /** @type {number} */
    var MIN_DISTANCE = 24 - (this.config.last_hour - this.config.first_hour);
    return !!(d > MIN_DISTANCE || c > a && r >= b);
  }
  return false;
}, scheduler.isOneDayEvent = function(ev) {
  /** @type {number} */
  var t = ev.end_date.getDate() - ev.start_date.getDate();
  return t ? (0 > t && (t = Math.ceil((ev.end_date.valueOf() - ev.start_date.valueOf()) / 864e5)), 1 == t && !ev.end_date.getHours() && !ev.end_date.getMinutes() && (ev.start_date.getHours() || ev.start_date.getMinutes())) : ev.start_date.getMonth() == ev.end_date.getMonth() && ev.start_date.getFullYear() == ev.end_date.getFullYear();
}, scheduler.get_visible_events = function(only_timed) {
  /** @type {!Array} */
  var result = [];
  var i;
  for (i in this._events) {
    if (this.is_visible_events(this._events[i]) && (!only_timed || this._events[i]._timed) && this.filter_event(i, this._events[i])) {
      result.push(this._events[i]);
    }
  }
  return result;
}, scheduler.filter_event = function(a, s) {
  var lf = this["filter_" + this._mode];
  return lf ? lf(a, s) : true;
}, scheduler._is_main_area_event = function(Visibility) {
  return !!Visibility._timed;
}, scheduler.render_view_data = function(evs, hold) {
  /** @type {boolean} */
  var k = false;
  if (!evs) {
    if (k = true, this._not_render) {
      return void(this._render_wait = true);
    }
    /** @type {boolean} */
    this._render_wait = false;
    this.clear_view();
    evs = this.get_visible_events(!(this._table_view || this.config.multi_day));
  }
  /** @type {number} */
  var i = 0;
  var len = evs.length;
  for (; len > i; i++) {
    this._recalculate_timed(evs[i]);
  }
  if (this.config.multi_day && !this._table_view) {
    /** @type {!Array} */
    var tvd = [];
    /** @type {!Array} */
    var tvs = [];
    /** @type {number} */
    i = 0;
    for (; i < evs.length; i++) {
      if (this._is_main_area_event(evs[i])) {
        tvd.push(evs[i]);
      } else {
        tvs.push(evs[i]);
      }
    }
    this._rendered_location = this._els.dhx_multi_day[0];
    /** @type {boolean} */
    this._table_view = true;
    this.render_data(tvs, hold);
    /** @type {boolean} */
    this._table_view = false;
    this._rendered_location = this._els.dhx_cal_data[0];
    /** @type {boolean} */
    this._table_view = false;
    this.render_data(tvd, hold);
  } else {
    /** @type {!DocumentFragment} */
    var tableDataCellElementOne = document.createDocumentFragment();
    var tableRowElementOne = this._els.dhx_cal_data[0];
    /** @type {!DocumentFragment} */
    this._rendered_location = tableDataCellElementOne;
    this.render_data(evs, hold);
    tableRowElementOne.appendChild(tableDataCellElementOne);
    this._rendered_location = tableRowElementOne;
  }
  if (k) {
    this.callEvent("onDataRender", []);
  }
}, scheduler._view_month_day = function(e) {
  var data = scheduler.getActionData(e).date;
  if (scheduler.callEvent("onViewMoreClick", [data])) {
    scheduler.setCurrentView(data, "day");
  }
}, scheduler._render_month_link = function(options) {
  var recordsRoot = this._rendered_location;
  var self = this._lame_clone(options);
  var target = options._sday;
  for (; target < options._eday; target++) {
    self._sday = target;
    self._eday = target + 1;
    var date = scheduler.date;
    var start = scheduler._min_date;
    start = date.add(start, self._sweek, "week");
    start = date.add(start, self._sday, "day");
    var n = scheduler.getEvents(start, date.add(start, 1, "day")).length;
    var d = this._get_event_bar_pos(self);
    /** @type {number} */
    var bg_w = d.x2 - d.x;
    /** @type {!Element} */
    var result = document.createElement("div");
    /**
     * @param {string} ev
     * @return {undefined}
     */
    result.onclick = function(ev) {
      scheduler._view_month_day(ev || event);
    };
    /** @type {string} */
    result.className = "dhx_month_link";
    /** @type {string} */
    result.style.top = d.y + "px";
    /** @type {string} */
    result.style.left = d.x + "px";
    /** @type {string} */
    result.style.width = bg_w + "px";
    result.innerHTML = scheduler.templates.month_events_link(start, n);
    this._rendered.push(result);
    recordsRoot.appendChild(result);
  }
}, scheduler._recalculate_timed = function(key) {
  if (key) {
    var ev;
    ev = "object" != typeof key ? this._events[key] : key;
    if (ev) {
      ev._timed = scheduler.isOneDayEvent(ev);
    }
  }
}, scheduler.attachEvent("onEventChanged", scheduler._recalculate_timed), scheduler.attachEvent("onEventAdded", scheduler._recalculate_timed), scheduler.render_data = function(evs, hold) {
  evs = this._pre_render_events(evs, hold);
  var inputList = {};
  /** @type {number} */
  var i = 0;
  for (; i < evs.length; i++) {
    if (this._table_view) {
      if ("month" != scheduler._mode) {
        this.render_event_bar(evs[i]);
      } else {
        var h = scheduler.config.max_month_events;
        if (h !== 1 * h || evs[i]._sorder < h) {
          this.render_event_bar(evs[i]);
        } else {
          if (void 0 !== h && evs[i]._sorder == h) {
            scheduler._render_month_link(evs[i]);
          }
        }
      }
    } else {
      var ev = evs[i];
      var cropframe = scheduler.locate_holder(ev._sday);
      if (!cropframe) {
        continue;
      }
      if (!inputList[ev._sday]) {
        inputList[ev._sday] = {
          real : cropframe,
          buffer : document.createDocumentFragment(),
          width : cropframe.clientWidth
        };
      }
      var input = inputList[ev._sday];
      this.render_event(ev, input.buffer, input.width);
    }
  }
  for (i in inputList) {
    input = inputList[i];
    if (input.real && input.buffer) {
      input.real.appendChild(input.buffer);
    }
  }
}, scheduler._get_first_visible_cell = function(elms) {
  /** @type {number} */
  var i = 0;
  for (; i < elms.length; i++) {
    if (-1 == (elms[i].className || "").indexOf("dhx_scale_ignore")) {
      return elms[i];
    }
  }
  return elms[0];
}, scheduler._pre_render_events = function(evs, hold) {
  var hb = this.xy.bar_height;
  var h_old = this._colsS.heights;
  /** @type {!Array} */
  var h = this._colsS.heights = [0, 0, 0, 0, 0, 0, 0];
  var div = this._els.dhx_cal_data[0];
  if (evs = this._table_view ? this._pre_render_events_table(evs, hold) : this._pre_render_events_line(evs, hold), this._table_view) {
    if (hold) {
      this._colsS.heights = h_old;
    } else {
      var e = div.firstChild;
      if (e.rows) {
        /** @type {number} */
        var i = 0;
        for (; i < e.rows.length; i++) {
          h[i]++;
          var cells = e.rows[i].cells;
          /** @type {number} */
          var editorInitialHeightDefault = this._colsS.height - this.xy.month_head_height;
          if (h[i] * hb > editorInitialHeightDefault) {
            /** @type {number} */
            var actualVideoHeight = editorInitialHeightDefault;
            if (1 * this.config.max_month_events !== this.config.max_month_events || h[i] <= this.config.max_month_events) {
              /** @type {number} */
              actualVideoHeight = h[i] * hb;
            } else {
              if ((this.config.max_month_events + 1) * hb > editorInitialHeightDefault) {
                /** @type {number} */
                actualVideoHeight = (this.config.max_month_events + 1) * hb;
              }
            }
            /** @type {number} */
            var j = 0;
            for (; j < cells.length; j++) {
              /** @type {string} */
              cells[j].childNodes[1].style.height = actualVideoHeight + "px";
            }
          }
          h[i] = (h[i - 1] || 0) + scheduler._get_first_visible_cell(cells).offsetHeight;
        }
        if (h.unshift(0), e.parentNode.offsetHeight < e.parentNode.scrollHeight && !scheduler._colsS.scroll_fix && scheduler.xy.scroll_width) {
          var t = scheduler._colsS;
          var val = t[t.col_length];
          var h_old = t.heights.slice();
          /** @type {number} */
          val = val - (scheduler.xy.scroll_width || 0);
          this._calc_scale_sizes(val, this._min_date, this._max_date);
          scheduler._colsS.heights = h_old;
          this.set_xy(this._els.dhx_cal_header[0], val, this.xy.scale_height);
          scheduler._render_scales(this._els.dhx_cal_header[0]);
          scheduler._render_month_scale(this._els.dhx_cal_data[0], this._get_timeunit_start(), this._min_date);
          /** @type {boolean} */
          t.scroll_fix = true;
        }
      } else {
        if (evs.length || "visible" != this._els.dhx_multi_day[0].style.visibility || (h[0] = -1), evs.length || -1 == h[0]) {
          /** @type {number} */
          var v = (e.parentNode.childNodes, (h[0] + 1) * hb + 1);
          /** @type {number} */
          var value = v;
          /** @type {string} */
          var val = v + "px";
          if (this.config.multi_day_height_limit) {
            /** @type {number} */
            value = Math.min(v, this.config.multi_day_height_limit);
            /** @type {string} */
            val = value + "px";
          }
          /** @type {string} */
          div.style.top = this._els.dhx_cal_navline[0].offsetHeight + this._els.dhx_cal_header[0].offsetHeight + value + "px";
          /** @type {string} */
          div.style.height = this._obj.offsetHeight - parseInt(div.style.top, 10) - (this.xy.margin_top || 0) + "px";
          var tooltipDiv = this._els.dhx_multi_day[0];
          /** @type {string} */
          tooltipDiv.style.height = val;
          /** @type {string} */
          tooltipDiv.style.visibility = -1 == h[0] ? "hidden" : "visible";
          var last = this._els.dhx_multi_day[1];
          /** @type {string} */
          last.style.height = val;
          /** @type {string} */
          last.style.visibility = -1 == h[0] ? "hidden" : "visible";
          /** @type {string} */
          last.className = h[0] ? "dhx_multi_day_icon" : "dhx_multi_day_icon_small";
          /** @type {number} */
          this._dy_shift = (h[0] + 1) * hb;
          if (this.config.multi_day_height_limit) {
            /** @type {number} */
            this._dy_shift = Math.min(this.config.multi_day_height_limit, this._dy_shift);
          }
          /** @type {number} */
          h[0] = 0;
          if (value != v) {
            /** @type {string} */
            div.style.top = parseInt(div.style.top) + 2 + "px";
            /** @type {string} */
            tooltipDiv.style.overflowY = "auto";
            /** @type {string} */
            last.style.position = "fixed";
            /** @type {string} */
            last.style.top = "";
            /** @type {string} */
            last.style.left = "";
          }
        }
      }
    }
  }
  return evs;
}, scheduler._get_event_sday = function(ev) {
  var petNameAsDate = this.date.day_start(new Date(ev.start_date));
  return Math.round((petNameAsDate.valueOf() - this._min_date.valueOf()) / 864e5);
}, scheduler._get_event_mapped_end_date = function(ev) {
  var dt = ev.end_date;
  if (this.config.separate_short_events) {
    /** @type {number} */
    var j = (ev.end_date - ev.start_date) / 6e4;
    if (j < this._min_mapped_duration) {
      dt = this.date.add(dt, this._min_mapped_duration - j, "minute");
    }
  }
  return dt;
}, scheduler._pre_render_events_line = function(evs, hold) {
  evs.sort(function(a, b) {
    return a.start_date.valueOf() == b.start_date.valueOf() ? a.id > b.id ? 1 : -1 : a.start_date > b.start_date ? 1 : -1;
  });
  /** @type {!Array} */
  var hook = [];
  /** @type {!Array} */
  var dequeue = [];
  /** @type {number} */
  this._min_mapped_duration = Math.ceil(60 * this.xy.min_event_height / this.config.hour_size_px);
  /** @type {number} */
  var i = 0;
  for (; i < evs.length; i++) {
    var ev = evs[i];
    var d = ev.start_date;
    var context = ev.end_date;
    var major = d.getHours();
    var level = context.getHours();
    if (ev._sday = this._get_event_sday(ev), this._ignores[ev._sday]) {
      evs.splice(i, 1);
      i--;
    } else {
      if (hook[ev._sday] || (hook[ev._sday] = []), !hold) {
        /** @type {boolean} */
        ev._inner = false;
        var stack = hook[ev._sday];
        for (; stack.length;) {
          var e = stack[stack.length - 1];
          var c = this._get_event_mapped_end_date(e);
          if (!(c.valueOf() <= ev.start_date.valueOf())) {
            break;
          }
          stack.splice(stack.length - 1, 1);
        }
        var i = stack.length;
        /** @type {boolean} */
        var g = false;
        /** @type {number} */
        var h = 0;
        for (; h < stack.length; h++) {
          e = stack[h];
          c = this._get_event_mapped_end_date(e);
          if (c.valueOf() <= ev.start_date.valueOf()) {
            /** @type {boolean} */
            g = true;
            ev._sorder = e._sorder;
            /** @type {number} */
            i = h;
            /** @type {boolean} */
            ev._inner = true;
            break;
          }
        }
        if (stack.length && (stack[stack.length - 1]._inner = true), !g) {
          if (stack.length) {
            if (stack.length <= stack[stack.length - 1]._sorder) {
              if (stack[stack.length - 1]._sorder) {
                /** @type {number} */
                h = 0;
                for (; h < stack.length; h++) {
                  /** @type {boolean} */
                  var v = false;
                  /** @type {number} */
                  var w = 0;
                  for (; w < stack.length; w++) {
                    if (stack[w]._sorder == h) {
                      /** @type {boolean} */
                      v = true;
                      break;
                    }
                  }
                  if (!v) {
                    /** @type {number} */
                    ev._sorder = h;
                    break;
                  }
                }
              } else {
                /** @type {number} */
                ev._sorder = 0;
              }
              /** @type {boolean} */
              ev._inner = true;
            } else {
              var _max_sorder = stack[0]._sorder;
              /** @type {number} */
              h = 1;
              for (; h < stack.length; h++) {
                if (stack[h]._sorder > _max_sorder) {
                  _max_sorder = stack[h]._sorder;
                }
              }
              ev._sorder = _max_sorder + 1;
              /** @type {boolean} */
              ev._inner = false;
            }
          } else {
            /** @type {number} */
            ev._sorder = 0;
          }
        }
        stack.splice(i, i == stack.length ? 0 : 1, ev);
        if (stack.length > (stack.max_count || 0)) {
          stack.max_count = stack.length;
          ev._count = stack.length;
        } else {
          ev._count = ev._count ? ev._count : 1;
        }
      }
      if ((major < this.config.first_hour || level >= this.config.last_hour) && (dequeue.push(ev), evs[i] = ev = this._copy_event(ev), major < this.config.first_hour && (ev.start_date.setHours(this.config.first_hour), ev.start_date.setMinutes(0)), level >= this.config.last_hour && (ev.end_date.setMinutes(0), ev.end_date.setHours(this.config.last_hour)), ev.start_date > ev.end_date || major == this.config.last_hour)) {
        evs.splice(i, 1);
        i--;
      }
    }
  }
  if (!hold) {
    /** @type {number} */
    i = 0;
    for (; i < evs.length; i++) {
      evs[i]._count = hook[evs[i]._sday].max_count;
    }
    /** @type {number} */
    i = 0;
    for (; i < dequeue.length; i++) {
      dequeue[i]._count = hook[dequeue[i]._sday].max_count;
    }
  }
  return evs;
}, scheduler._time_order = function(events) {
  events.sort(function(a, b) {
    return a.start_date.valueOf() == b.start_date.valueOf() ? a._timed && !b._timed ? 1 : !a._timed && b._timed ? -1 : a.id > b.id ? 1 : -1 : a.start_date > b.start_date ? 1 : -1;
  });
}, scheduler._is_any_multiday_cell_visible = function(date, text, name) {
  var l = this._cols.length;
  /** @type {boolean} */
  var s = false;
  /** @type {!Object} */
  var day = date;
  /** @type {boolean} */
  var g = true;
  for (; text > day;) {
    /** @type {boolean} */
    g = false;
    var index = this.locate_holder_day(day, false, name);
    /** @type {number} */
    var i = index % l;
    if (!this._ignores[i]) {
      /** @type {boolean} */
      s = true;
      break;
    }
    day = scheduler.date.add(day, 1, "day");
  }
  return g || s;
}, scheduler._pre_render_events_table = function(evs, hold) {
  this._time_order(evs);
  var start_date;
  /** @type {!Array} */
  var q = [];
  /** @type {!Array} */
  var bindings = [[], [], [], [], [], [], []];
  var h_old = this._colsS.heights;
  var cols = this._cols.length;
  var installedModules = {};
  /** @type {number} */
  var i = 0;
  for (; i < evs.length; i++) {
    var ev = evs[i];
    var moduleId = ev.id;
    if (!installedModules[moduleId]) {
      installedModules[moduleId] = {
        first_chunk : true,
        last_chunk : true
      };
    }
    var me = installedModules[moduleId];
    var start = start_date || ev.start_date;
    var day = ev.end_date;
    if (start < this._min_date) {
      /** @type {boolean} */
      me.first_chunk = false;
      start = this._min_date;
    }
    if (day > this._max_date) {
      /** @type {boolean} */
      me.last_chunk = false;
      day = this._max_date;
    }
    var cycle = this.locate_holder_day(start, false, ev);
    if (ev._sday = cycle % cols, !this._ignores[ev._sday] || !ev._timed) {
      var key = this.locate_holder_day(day, true, ev) || cols;
      ev._eday = key % cols || cols;
      /** @type {number} */
      ev._length = key - cycle;
      /** @type {number} */
      ev._sweek = Math.floor((this._correct_shift(start.valueOf(), 1) - this._min_date.valueOf()) / (864e5 * cols));
      var startday = scheduler._is_any_multiday_cell_visible(start, day, ev);
      if (startday) {
        var key;
        var obj = bindings[ev._sweek];
        /** @type {number} */
        key = 0;
        for (; key < obj.length && !(obj[key]._eday <= ev._sday); key++) {
        }
        if (ev._sorder && hold || (ev._sorder = key), ev._sday + ev._length <= cols) {
          /** @type {null} */
          start_date = null;
          q.push(ev);
          obj[key] = ev;
          /** @type {number} */
          h_old[ev._sweek] = obj.length - 1;
          ev._first_chunk = me.first_chunk;
          ev._last_chunk = me.last_chunk;
        } else {
          var copy = this._copy_event(ev);
          copy.id = ev.id;
          /** @type {number} */
          copy._length = cols - ev._sday;
          copy._eday = cols;
          /** @type {number} */
          copy._sday = ev._sday;
          /** @type {number} */
          copy._sweek = ev._sweek;
          copy._sorder = ev._sorder;
          copy.end_date = this.date.add(start, copy._length, "day");
          copy._first_chunk = me.first_chunk;
          if (me.first_chunk) {
            /** @type {boolean} */
            me.first_chunk = false;
          }
          q.push(copy);
          obj[key] = copy;
          start_date = copy.end_date;
          /** @type {number} */
          h_old[ev._sweek] = obj.length - 1;
          i--;
        }
      }
    }
  }
  return q;
}, scheduler._copy_dummy = function() {
  /** @type {!Date} */
  var start_date = new Date(this.start_date);
  /** @type {!Date} */
  var end_date = new Date(this.end_date);
  /** @type {!Date} */
  this.start_date = start_date;
  /** @type {!Date} */
  this.end_date = end_date;
}, scheduler._copy_event = function(x) {
  return this._copy_dummy.prototype = x, new this._copy_dummy;
}, scheduler._rendered = [], scheduler.clear_view = function() {
  /** @type {number} */
  var k = 0;
  for (; k < this._rendered.length; k++) {
    var t = this._rendered[k];
    if (t.parentNode) {
      t.parentNode.removeChild(t);
    }
  }
  /** @type {!Array} */
  this._rendered = [];
}, scheduler.updateEvent = function(id) {
  var data = this.getEvent(id);
  this.clear_event(id);
  if (data && this.is_visible_events(data) && this.filter_event(id, data) && (this._table_view || this.config.multi_day || data._timed)) {
    if (this.config.update_render) {
      this.render_view_data();
    } else {
      if ("month" != this.getState().mode || this.getState().drag_id || this.isOneDayEvent(data)) {
        this.render_view_data([data], true);
      } else {
        this.render_view_data();
      }
    }
  }
}, scheduler.clear_event = function(event_id) {
  this.for_rendered(event_id, function(gapiEl, idxC) {
    if (gapiEl.parentNode) {
      gapiEl.parentNode.removeChild(gapiEl);
    }
    scheduler._rendered.splice(idxC, 1);
  });
}, scheduler._y_from_date = function(ca) {
  var t = 60 * ca.getHours() + ca.getMinutes();
  return Math.round((60 * t * 1e3 - 60 * this.config.first_hour * 60 * 1e3) * this.config.hour_size_px / 36e5) % (24 * this.config.hour_size_px);
}, scheduler._calc_event_y = function(event, level) {
  level = level || 0;
  var trigger_gap = 60 * event.start_date.getHours() + event.start_date.getMinutes();
  var day = 60 * event.end_date.getHours() + event.end_date.getMinutes() || 60 * scheduler.config.last_hour;
  var tabPadding = this._y_from_date(event.start_date);
  /** @type {number} */
  var tileHeight = Math.max(level, (day - trigger_gap) * this.config.hour_size_px / 60);
  return {
    top : tabPadding,
    height : tileHeight
  };
}, scheduler.render_event = function(ev, ctx, width) {
  var w = scheduler.xy.menu_width;
  var size = this.config.use_select_menu_space ? 0 : w;
  if (!(ev._sday < 0)) {
    var img = scheduler.locate_holder(ev._sday);
    if (img) {
      ctx = ctx || img;
      var target = this._calc_event_y(ev, scheduler.xy.min_event_height);
      var y = target.top;
      var maxY = target.height;
      var ncols = ev._count || 1;
      var h = ev._sorder || 0;
      width = width || img.clientWidth;
      /** @type {number} */
      var w = Math.floor((width - size) / ncols);
      /** @type {number} */
      var x = h * w + 1;
      if (ev._inner || (w = w * (ncols - h)), this.config.cascade_event_display) {
        var c = this.config.cascade_event_count;
        var s = this.config.cascade_event_margin;
        /** @type {number} */
        x = h % c * s;
        /** @type {number} */
        var x2 = ev._inner ? (ncols - h - 1) % c * s / 2 : 0;
        /** @type {number} */
        w = Math.floor(width - size - x - x2);
      }
      var data = this._render_v_bar(ev, size + x, y, w, maxY, ev._text_style, scheduler.templates.event_header(ev.start_date, ev.end_date, ev), scheduler.templates.event_text(ev.start_date, ev.end_date, ev));
      if (this._waiAria.eventAttr(ev, data), this._rendered.push(data), ctx.appendChild(data), x = x + parseInt(img.style.left, 10) + size, this._edit_id == ev.id) {
        /** @type {number} */
        data.style.zIndex = 1;
        /** @type {number} */
        w = Math.max(w - 4, scheduler.xy.editor_width);
        /** @type {!Element} */
        data = document.createElement("div");
        data.setAttribute("event_id", ev.id);
        this._waiAria.eventAttr(ev, data);
        this.set_xy(data, w, maxY - 20, x, y + (scheduler.xy.event_header_height || 14));
        /** @type {string} */
        data.className = "dhx_cal_event dhx_cal_editor";
        if (ev.color) {
          data.style.backgroundColor = ev.color;
        }
        var cs = scheduler.templates.event_class(ev.start_date, ev.end_date, ev);
        if (cs) {
          data.className += " " + cs;
        }
        /** @type {!Element} */
        var container = document.createElement("div");
        this.set_xy(container, w - 6, maxY - 26);
        container.style.cssText += ";margin:2px 2px 2px 2px;overflow:hidden;";
        data.appendChild(container);
        this._els.dhx_cal_data[0].appendChild(data);
        this._rendered.push(data);
        /** @type {string} */
        container.innerHTML = "<textarea class='dhx_cal_editor'>" + ev.text + "</textarea>";
        if (this._quirks7) {
          /** @type {string} */
          container.firstChild.style.height = maxY - 12 + "px";
        }
        /** @type {(Node|null)} */
        this._editor = container.firstChild;
        /**
         * @param {!Object} e
         * @return {?}
         */
        this._editor.onkeydown = function(e) {
          if ((e || event).shiftKey) {
            return true;
          }
          var key = (e || event).keyCode;
          if (key == scheduler.keys.edit_save) {
            scheduler.editStop(true);
          }
          if (key == scheduler.keys.edit_cancel) {
            scheduler.editStop(false);
          }
          if ((key == scheduler.keys.edit_save || key == scheduler.keys.edit_cancel) && e.preventDefault) {
            e.preventDefault();
          }
        };
        /**
         * @param {string} e
         * @return {?}
         */
        this._editor.onselectstart = function(e) {
          return (e || event).cancelBubble = true, true;
        };
        scheduler._focus(container.firstChild, true);
        /** @type {number} */
        this._els.dhx_cal_data[0].scrollLeft = 0;
      }
      if (0 !== this.xy.menu_width && this._select_id == ev.id) {
        if (this.config.cascade_event_display && this._drag_mode) {
          /** @type {number} */
          data.style.zIndex = 1;
        }
        var b;
        var prof = this.config["icons_" + (this._edit_id == ev.id ? "edit" : "select")];
        /** @type {string} */
        var images = "";
        /** @type {string} */
        var port = ev.color ? "background-color: " + ev.color + ";" : "";
        /** @type {string} */
        var url = ev.textColor ? "color: " + ev.textColor + ";" : "";
        /** @type {number} */
        var i = 0;
        for (; i < prof.length; i++) {
          b = this._waiAria.eventMenuAttrString(prof[i]);
          /** @type {string} */
          images = images + ("<div class='dhx_menu_icon " + prof[i] + "' style='" + port + url + "' title='" + this.locale.labels[prof[i]] + "'" + b + "></div>");
        }
        var result = this._render_v_bar(ev, x - w + 1, y, w, 20 * prof.length + 26 - 2, "", "<div style='" + port + url + "' class='dhx_menu_head'></div>", images, true);
        /** @type {number} */
        result.style.left = x - w + 1;
        this._els.dhx_cal_data[0].appendChild(result);
        this._rendered.push(result);
      }
      if (this.config.drag_highlight && this._drag_id == ev.id) {
        this.highlightEventPosition(ev);
      }
    }
  }
}, scheduler._render_v_bar = function(ev, op, b, mode, event, message, immediate, name, err) {
  /** @type {!Element} */
  var a = document.createElement("div");
  var source = ev.id;
  /** @type {string} */
  var msg = err ? "dhx_cal_event dhx_cal_select_menu" : "dhx_cal_event";
  var options = scheduler.getState();
  if (options.drag_id == ev.id) {
    /** @type {string} */
    msg = msg + " dhx_cal_event_drag";
  }
  if (options.select_id == ev.id) {
    /** @type {string} */
    msg = msg + " dhx_cal_event_selected";
  }
  var text = scheduler.templates.event_class(ev.start_date, ev.end_date, ev);
  if (text) {
    /** @type {string} */
    msg = msg + " " + text;
  }
  if (this.config.cascade_event_display) {
    /** @type {string} */
    msg = msg + " dhx_cal_event_cascade";
  }
  /** @type {string} */
  var port = ev.color ? "background-color:" + ev.color + ";" : "";
  /** @type {string} */
  var url = ev.textColor ? "color:" + ev.textColor + ";" : "";
  var point = scheduler._border_box_bvents();
  /** @type {number} */
  var flipback180 = mode - 2;
  /** @type {number} */
  var x = point ? flipback180 : mode - 4;
  /** @type {number} */
  var properties = point ? flipback180 : mode - 6;
  /** @type {number} */
  var aniBName = point ? flipback180 : mode - (this._quirks ? 4 : 14);
  /** @type {number} */
  var y = point ? flipback180 - 2 : mode - 8;
  /** @type {number} */
  var nodeFn0 = point ? event - this.xy.event_header_height - 1 : event - (this._quirks ? 20 : 30) + 1;
  /** @type {string} */
  var entite = '<div event_id="' + source + '" class="' + msg + '" style="position:absolute; top:' + b + "px; left:" + op + "px; width:" + x + "px; height:" + event + "px;" + (message || "") + '"></div>';
  /** @type {string} */
  a.innerHTML = entite;
  /** @type {(Node|null)} */
  var d = a.cloneNode(true).firstChild;
  if (!err && scheduler.renderEvent(d, ev, mode, event, immediate, name)) {
    return d;
  }
  /** @type {(Node|null)} */
  d = a.firstChild;
  /** @type {string} */
  var helpTextData = '<div class="dhx_event_move dhx_header" style=" width:' + properties + "px;" + port + '" >&nbsp;</div>';
  /** @type {string} */
  helpTextData = helpTextData + ('<div class="dhx_event_move dhx_title" style="' + port + url + '">' + immediate + "</div>");
  /** @type {string} */
  helpTextData = helpTextData + ('<div class="dhx_body" style=" width:' + aniBName + "px; height:" + nodeFn0 + "px;" + port + url + '">' + name + "</div>");
  /** @type {string} */
  var roundednumber = "dhx_event_resize dhx_footer";
  return (err || ev._drag_resize === false) && (roundednumber = "dhx_resize_denied " + roundednumber), helpTextData = helpTextData + ('<div class="' + roundednumber + '" style=" width:' + y + "px;" + (err ? " margin-top:-1px;" : "") + port + url + '" ></div>'), d.innerHTML = helpTextData, d;
}, scheduler.renderEvent = function() {
  return false;
}, scheduler.locate_holder = function(indexColumn) {
  return "day" == this._mode ? this._els.dhx_cal_data[0].firstChild : this._els.dhx_cal_data[0].childNodes[indexColumn];
}, scheduler.locate_holder_day = function(day, earliest) {
  /** @type {number} */
  var i = Math.floor((this._correct_shift(day, 1) - this._min_date) / 864e5);
  return earliest && this.date.time_part(day) && i++, i;
}, scheduler._get_dnd_order = function(e, context, lambdaCallback) {
  if (!this._drag_event) {
    return e;
  }
  if (this._drag_event._orig_sorder) {
    e = this._drag_event._orig_sorder;
  } else {
    /** @type {number} */
    this._drag_event._orig_sorder = e;
  }
  /** @type {number} */
  var lineno = context * e;
  for (; lineno + context > lambdaCallback;) {
    e--;
    /** @type {number} */
    lineno = lineno - context;
  }
  return e = Math.max(e, 0);
}, scheduler._get_event_bar_pos = function(ev) {
  var right = this._colsS[ev._sday];
  var left = this._colsS[ev._eday];
  if (left == right) {
    left = this._colsS[ev._eday + 1];
  }
  var hb = this.xy.bar_height;
  var id = ev._sorder;
  if (ev.id == this._drag_id) {
    /** @type {number} */
    var callback = this._colsS.heights[ev._sweek + 1] - this._colsS.heights[ev._sweek] - this.xy.month_head_height;
    id = scheduler._get_dnd_order(id, hb, callback);
  }
  /** @type {number} */
  var baseName = id * hb;
  var middlePathName = this._colsS.heights[ev._sweek] + (this._colsS.height ? this.xy.month_scale_height + 2 : 2) + baseName;
  return {
    x : right,
    x2 : left,
    y : middlePathName
  };
}, scheduler.render_event_bar = function(ev) {
  var htmlNode = this._rendered_location;
  var c = this._get_event_bar_pos(ev);
  var nodeTly = c.y;
  var cx = c.x;
  var x = c.x2;
  /** @type {string} */
  var prevBondStereoStr = "";
  if (x) {
    var d = scheduler.config.resize_month_events && "month" == this._mode && (!ev._timed || scheduler.config.resize_month_timed);
    /** @type {!Element} */
    var o = document.createElement("div");
    var modifierKeyPressed = ev.hasOwnProperty("_first_chunk") && ev._first_chunk;
    var POINTER_MOUSE = ev.hasOwnProperty("_last_chunk") && ev._last_chunk;
    var val = d && (ev._timed || modifierKeyPressed);
    var v = d && (ev._timed || POINTER_MOUSE);
    /** @type {string} */
    var stringExpr = "dhx_cal_event_clear";
    if (!ev._timed || d) {
      /** @type {string} */
      stringExpr = "dhx_cal_event_line";
    }
    if (modifierKeyPressed) {
      /** @type {string} */
      stringExpr = stringExpr + " dhx_cal_event_line_start";
    }
    if (POINTER_MOUSE) {
      /** @type {string} */
      stringExpr = stringExpr + " dhx_cal_event_line_end";
    }
    if (val) {
      /** @type {string} */
      prevBondStereoStr = prevBondStereoStr + "<div class='dhx_event_resize dhx_event_resize_start'></div>";
    }
    if (v) {
      /** @type {string} */
      prevBondStereoStr = prevBondStereoStr + "<div class='dhx_event_resize dhx_event_resize_end'></div>";
    }
    var quoteChar = scheduler.templates.event_class(ev.start_date, ev.end_date, ev);
    if (quoteChar) {
      /** @type {string} */
      stringExpr = stringExpr + (" " + quoteChar);
    }
    /** @type {string} */
    var inlineClass = ev.color ? "background:" + ev.color + ";" : "";
    /** @type {string} */
    var flipYPart = ev.textColor ? "color:" + ev.textColor + ";" : "";
    /** @type {string} */
    var m = ["position:absolute", "top:" + nodeTly + "px", "left:" + cx + "px", "width:" + (x - cx - 15) + "px", flipYPart, inlineClass, ev._text_style || ""].join(";");
    /** @type {string} */
    var result = "<div event_id='" + ev.id + "' class='" + stringExpr + "' style='" + m + "'" + this._waiAria.eventBarAttrString(ev) + ">";
    if (d) {
      /** @type {string} */
      result = result + prevBondStereoStr;
    }
    if ("month" == scheduler.getState().mode) {
      ev = scheduler.getEvent(ev.id);
    }
    if (ev._timed) {
      result = result + scheduler.templates.event_bar_date(ev.start_date, ev.end_date, ev);
    }
    result = result + (scheduler.templates.event_bar_text(ev.start_date, ev.end_date, ev) + "</div>");
    /** @type {string} */
    result = result + "</div>";
    /** @type {string} */
    o.innerHTML = result;
    this._rendered.push(o.firstChild);
    htmlNode.appendChild(o.firstChild);
  }
}, scheduler._locate_event = function(t) {
  /** @type {null} */
  var el = null;
  for (; t && !el && t.getAttribute;) {
    el = t.getAttribute("event_id");
    t = t.parentNode;
  }
  return el;
}, scheduler._locate_css = function(e, d, lazyLayout) {
  if (void 0 === lazyLayout) {
    /** @type {boolean} */
    lazyLayout = true;
  }
  var item = e.target || e.srcElement;
  /** @type {string} */
  var s = "";
  for (; item;) {
    if (s = scheduler._getClassName(item)) {
      var len = s.indexOf(d);
      if (len >= 0) {
        if (!lazyLayout) {
          return item;
        }
        /** @type {boolean} */
        var n = 0 === len || !scheduler._trim(s.charAt(len - 1));
        /** @type {boolean} */
        var e = len + d.length >= s.length || !scheduler._trim(s.charAt(len + d.length));
        if (n && e) {
          return item;
        }
      }
    }
    item = item.parentNode;
  }
  return null;
}, scheduler.edit = function(c) {
  if (this._edit_id != c) {
    this.editStop(false, c);
    /** @type {string} */
    this._edit_id = c;
    this.updateEvent(c);
  }
}, scheduler.editStop = function(mode, strategy) {
  if (!strategy || this._edit_id != strategy) {
    var ce = this.getEvent(this._edit_id);
    if (ce) {
      if (mode) {
        ce.text = this._editor.value;
      }
      /** @type {null} */
      this._edit_id = null;
      /** @type {null} */
      this._editor = null;
      this.updateEvent(ce.id);
      this._edit_stop_event(ce, mode);
    }
  }
}, scheduler._edit_stop_event = function(el, steps) {
  if (this._new_event) {
    if (steps) {
      this.callEvent("onEventAdded", [el.id, el]);
    } else {
      if (el) {
        this.deleteEvent(el.id, true);
      }
    }
    /** @type {null} */
    this._new_event = null;
  } else {
    if (steps) {
      this.callEvent("onEventChanged", [el.id, el]);
    }
  }
}, scheduler.getEvents = function(from, to) {
  /** @type {!Array} */
  var result = [];
  var i;
  for (i in this._events) {
    var ev = this._events[i];
    if (ev && (!from && !to || ev.start_date < to && ev.end_date > from)) {
      result.push(ev);
    }
  }
  return result;
}, scheduler.getRenderedEvent = function(event_id) {
  if (event_id) {
    var evs = scheduler._rendered;
    /** @type {number} */
    var i = 0;
    for (; i < evs.length; i++) {
      var t = evs[i];
      if (t.getAttribute("event_id") == event_id) {
        return t;
      }
    }
    return null;
  }
}, scheduler.showEvent = function(e, index) {
  var ev = "number" == typeof e || "string" == typeof e ? scheduler.getEvent(e) : e;
  if (index = index || scheduler._mode, ev && (!this.checkEvent("onBeforeEventDisplay") || this.callEvent("onBeforeEventDisplay", [ev, index]))) {
    var r = scheduler.config.scroll_hour;
    scheduler.config.scroll_hour = ev.start_date.getHours();
    var s = scheduler.config.preserve_scroll;
    /** @type {boolean} */
    scheduler.config.preserve_scroll = false;
    var value = ev.color;
    var textColor = ev.textColor;
    if (scheduler.config.highlight_displayed_event && (ev.color = scheduler.config.displayed_event_color, ev.textColor = scheduler.config.displayed_event_text_color), scheduler.setCurrentView(new Date(ev.start_date), index), ev.color = value, ev.textColor = textColor, scheduler.config.scroll_hour = r, scheduler.config.preserve_scroll = s, scheduler.matrix && scheduler.matrix[index]) {
      var container = scheduler.getRenderedEvent(ev.id);
      if (container) {
        /** @type {number} */
        scheduler._els.dhx_cal_data[0].scrollTop = scheduler.$domHelpers.getAbsoluteTop(container) - scheduler.$domHelpers.getAbsoluteTop(scheduler._els.dhx_cal_data[0]) - 20;
      }
    }
    scheduler.callEvent("onAfterEventDisplay", [ev, index]);
  }
}, scheduler._append_drag_marker = function(b) {
  if (!b.parentNode) {
    var t = scheduler._els.dhx_cal_data[0];
    var i = t.lastChild;
    var atomType = scheduler._getClassName(i);
    if (atomType.indexOf("dhx_scale_holder") < 0 && i.previousSibling) {
      i = i.previousSibling;
    }
    atomType = scheduler._getClassName(i);
    if (i && 0 === atomType.indexOf("dhx_scale_holder")) {
      i.appendChild(b);
    }
  }
}, scheduler._update_marker_position = function(img, data) {
  var i = scheduler._calc_event_y(data, 0);
  /** @type {string} */
  img.style.top = i.top + "px";
  /** @type {string} */
  img.style.height = i.height + "px";
}, scheduler.highlightEventPosition = function(task) {
  /** @type {!Element} */
  var t = document.createElement("div");
  t.setAttribute("event_id", task.id);
  this._rendered.push(t);
  this._update_marker_position(t, task);
  var p = this.templates.drag_marker_class(task.start_date, task.end_date, task);
  var template = this.templates.drag_marker_content(task.start_date, task.end_date, task);
  /** @type {string} */
  t.className = "dhx_drag_marker";
  if (p) {
    t.className += " " + p;
  }
  if (template) {
    t.innerHTML = template;
  }
  this._append_drag_marker(t);
}, scheduler._loaded = {}, scheduler._load = function(url, now) {
  if (url = url || this._load_url) {
    /** @type {string} */
    url = url + ((-1 == url.indexOf("?") ? "?" : "&") + "timeshift=" + (new Date).getTimezoneOffset());
    if (this.config.prevent_cache) {
      /** @type {string} */
      url = url + ("&uid=" + this.uid());
    }
    var date;
    if (now = now || this._date, this._load_mode) {
      var func = this.templates.load_format;
      now = this.date[this._load_mode + "_start"](new Date(now.valueOf()));
      for (; now > this._min_date;) {
        now = this.date.add(now, -1, this._load_mode);
      }
      /** @type {number} */
      date = now;
      /** @type {boolean} */
      var s = true;
      for (; date < this._max_date;) {
        date = this.date.add(date, 1, this._load_mode);
        if (this._loaded[func(now)] && s) {
          now = this.date.add(now, 1, this._load_mode);
        } else {
          /** @type {boolean} */
          s = false;
        }
      }
      var d = date;
      do {
        date = d;
        d = this.date.add(date, -1, this._load_mode);
      } while (d > now && this._loaded[func(d)]);
      if (now >= date) {
        return false;
      }
      scheduler.$ajax.get(url + "&from=" + func(now) + "&to=" + func(date), function(e) {
        scheduler.on_load(e);
      });
      for (; date > now;) {
        /** @type {boolean} */
        this._loaded[func(now)] = true;
        now = this.date.add(now, 1, this._load_mode);
      }
    } else {
      scheduler.$ajax.get(url, function(e) {
        scheduler.on_load(e);
      });
    }
    return this.callEvent("onXLS", []), true;
  }
}, scheduler.on_load = function(error) {
  var temp;
  /** @type {boolean} */
  var i = false;
  if (this._process && "xml" != this._process) {
    try {
      temp = this[this._process].parse(error.xmlDoc.responseText);
    } catch (r) {
      /** @type {boolean} */
      i = true;
    }
  } else {
    temp = this._magic_parser(error);
    if (!temp) {
      /** @type {boolean} */
      i = true;
    }
  }
  if (i || error.xmlDoc.status && error.xmlDoc.status >= 400) {
    this.callEvent("onLoadError", [error.xmlDoc]);
    /** @type {!Array} */
    temp = [];
  }
  scheduler._process_loading(temp);
  this.callEvent("onXLE", []);
}, scheduler._process_loading = function(name) {
  /** @type {boolean} */
  this._loading = true;
  /** @type {boolean} */
  this._not_render = true;
  /** @type {number} */
  var i = 0;
  for (; i < name.length; i++) {
    if (this.callEvent("onEventLoading", [name[i]])) {
      this.addEvent(name[i]);
    }
  }
  /** @type {boolean} */
  this._not_render = false;
  if (this._render_wait) {
    this.render_view_data();
  }
  /** @type {boolean} */
  this._loading = false;
  if (this._after_call) {
    this._after_call();
  }
  /** @type {null} */
  this._after_call = null;
}, scheduler._init_event = function(options) {
  options.text = options.text || options._tagvalue || "";
  options.start_date = scheduler._init_date(options.start_date);
  options.end_date = scheduler._init_date(options.end_date);
}, scheduler._init_date = function(data) {
  return data ? "string" == typeof data ? scheduler.templates.xml_date(data) : new Date(data) : null;
}, scheduler.json = {}, scheduler.json.parse = function(data$jscomp$32) {
  if ("string" == typeof data$jscomp$32) {
    if (window.JSON) {
      /** @type {*} */
      scheduler._temp = JSON.parse(data$jscomp$32);
    } else {
      /** @type {*} */
      scheduler._temp = eval("(" + data$jscomp$32 + ")");
    }
    data$jscomp$32 = scheduler._temp ? scheduler._temp.data || scheduler._temp.d || scheduler._temp : [];
  }
  if (data$jscomp$32.dhx_security) {
    dhtmlx.security_key = data$jscomp$32.dhx_security;
  }
  var collections$jscomp$0 = scheduler._temp && scheduler._temp.collections ? scheduler._temp.collections : {};
  /** @type {boolean} */
  var collections_loaded$jscomp$0 = false;
  var key$jscomp$35;
  for (key$jscomp$35 in collections$jscomp$0) {
    if (collections$jscomp$0.hasOwnProperty(key$jscomp$35)) {
      /** @type {boolean} */
      collections_loaded$jscomp$0 = true;
      var collection$jscomp$0 = collections$jscomp$0[key$jscomp$35];
      var arr$jscomp$8 = scheduler.serverList[key$jscomp$35];
      if (!arr$jscomp$8) {
        /** @type {!Array} */
        scheduler.serverList[key$jscomp$35] = arr$jscomp$8 = [];
      }
      arr$jscomp$8.splice(0, arr$jscomp$8.length);
      /** @type {number} */
      var j$jscomp$0 = 0;
      for (; j$jscomp$0 < collection$jscomp$0.length; j$jscomp$0++) {
        var option$jscomp$0 = collection$jscomp$0[j$jscomp$0];
        var obj$jscomp$27 = {
          key : option$jscomp$0.value,
          label : option$jscomp$0.label
        };
        var option_key$jscomp$0;
        for (option_key$jscomp$0 in option$jscomp$0) {
          if (option$jscomp$0.hasOwnProperty(option_key$jscomp$0)) {
            if ("value" == option_key$jscomp$0 || "label" == option_key$jscomp$0) {
              continue;
            }
            obj$jscomp$27[option_key$jscomp$0] = option$jscomp$0[option_key$jscomp$0];
          }
        }
        arr$jscomp$8.push(obj$jscomp$27);
      }
    }
  }
  if (collections_loaded$jscomp$0) {
    scheduler.callEvent("onOptionsLoad", []);
  }
  /** @type {!Array} */
  var evs$jscomp$0 = [];
  /** @type {number} */
  var i$jscomp$169 = 0;
  for (; i$jscomp$169 < data$jscomp$32.length; i$jscomp$169++) {
    var event$jscomp$0 = data$jscomp$32[i$jscomp$169];
    scheduler._init_event(event$jscomp$0);
    evs$jscomp$0.push(event$jscomp$0);
  }
  return evs$jscomp$0;
}, scheduler.parse = function(text, process) {
  /** @type {!Object} */
  this._process = process;
  this.on_load({
    xmlDoc : {
      responseText : text
    }
  });
}, scheduler.load = function(url, call) {
  if ("string" == typeof call) {
    /** @type {!Object} */
    this._process = call;
    call = arguments[2];
  }
  /** @type {string} */
  this._load_url = url;
  /** @type {!Object} */
  this._after_call = call;
  this._load(url, this._date);
}, scheduler.setLoadMode = function(queryType) {
  if ("all" == queryType) {
    /** @type {string} */
    queryType = "";
  }
  /** @type {string} */
  this._load_mode = queryType;
}, scheduler.serverList = function(idx, indent) {
  return indent ? (this.serverList[idx] = indent.slice(0), this.serverList[idx]) : (this.serverList[idx] = this.serverList[idx] || [], this.serverList[idx]);
}, scheduler._userdata = {}, scheduler._magic_parser = function(xml) {
  var v;
  if (xml.xmlDoc.responseXML || (xml.xmlDoc.responseXML = scheduler.$ajax.parse(xml.xmlDoc.responseText)), v = scheduler.$ajax.xmltop("data", xml.xmlDoc), "data" != v.tagName) {
    return null;
  }
  var i = v.getAttribute("dhx_security");
  if (i) {
    dhtmlx.security_key = i;
  }
  var cclass = scheduler.$ajax.xpath("//coll_options", xml.xmlDoc);
  /** @type {number} */
  var j = 0;
  for (; j < cclass.length; j++) {
    var name = cclass[j].getAttribute("for");
    var p = this.serverList[name];
    if (!p) {
      /** @type {!Array} */
      scheduler.serverList[name] = p = [];
    }
    p.splice(0, p.length);
    var features = scheduler.$ajax.xpath(".//item", cclass[j]);
    /** @type {number} */
    var i = 0;
    for (; i < features.length; i++) {
      var feature = features[i];
      var propertyAttributes = feature.attributes;
      var attributes = {
        key : features[i].getAttribute("value"),
        label : features[i].getAttribute("label")
      };
      /** @type {number} */
      var attributeIndex = 0;
      for (; attributeIndex < propertyAttributes.length; attributeIndex++) {
        var attribute = propertyAttributes[attributeIndex];
        if ("value" != attribute.nodeName && "label" != attribute.nodeName) {
          attributes[attribute.nodeName] = attribute.nodeValue;
        }
      }
      p.push(attributes);
    }
  }
  if (cclass.length) {
    scheduler.callEvent("onOptionsLoad", []);
  }
  var h = scheduler.$ajax.xpath("//userdata", xml.xmlDoc);
  /** @type {number} */
  j = 0;
  for (; j < h.length; j++) {
    var f = this._xmlNodeToJSON(h[j]);
    this._userdata[f.name] = f.text;
  }
  /** @type {!Array} */
  var nonDuplicateIds = [];
  v = scheduler.$ajax.xpath("//event", xml.xmlDoc);
  /** @type {number} */
  j = 0;
  for (; j < v.length; j++) {
    var formula = nonDuplicateIds[j] = this._xmlNodeToJSON(v[j]);
    scheduler._init_event(formula);
  }
  return nonDuplicateIds;
}, scheduler._xmlNodeToJSON = function(xmlNode) {
  var res = {};
  /** @type {number} */
  var i = 0;
  for (; i < xmlNode.attributes.length; i++) {
    res[xmlNode.attributes[i].name] = xmlNode.attributes[i].value;
  }
  /** @type {number} */
  i = 0;
  for (; i < xmlNode.childNodes.length; i++) {
    var data = xmlNode.childNodes[i];
    if (1 == data.nodeType) {
      res[data.tagName] = data.firstChild ? data.firstChild.nodeValue : "";
    }
  }
  return res.text || (res.text = xmlNode.firstChild ? xmlNode.firstChild.nodeValue : ""), res;
}, scheduler.attachEvent("onXLS", function() {
  if (this.config.show_loading === true) {
    var data;
    /** @type {!Element} */
    data = this.config.show_loading = document.createElement("div");
    /** @type {string} */
    data.className = "dhx_loading";
    /** @type {string} */
    data.style.left = Math.round((this._x - 128) / 2) + "px";
    /** @type {string} */
    data.style.top = Math.round((this._y - 15) / 2) + "px";
    this._obj.appendChild(data);
  }
}), scheduler.attachEvent("onXLE", function() {
  var t = this.config.show_loading;
  if (t && "object" == typeof t) {
    if (t.parentNode) {
      t.parentNode.removeChild(t);
    }
    /** @type {boolean} */
    this.config.show_loading = true;
  }
}), scheduler.ical = {
  parse : function(text) {
    var url = text.match(RegExp(this.c_start + "[^\f]*" + this.c_end, ""));
    if (url.length) {
      url[0] = url[0].replace(/[\r\n]+ /g, "");
      url[0] = url[0].replace(/[\r\n]+(?=[a-z \t])/g, " ");
      url[0] = url[0].replace(/;[^:\r\n]*:/g, ":");
      var response;
      /** @type {!Array} */
      var plist = [];
      /** @type {!RegExp} */
      var matcher = RegExp("(?:" + this.e_start + ")([^\f]*?)(?:" + this.e_end + ")", "g");
      for (; null !== (response = matcher.exec(url));) {
        var default_favicon;
        var p = {};
        /** @type {!RegExp} */
        var d = /[^\r\n]+[\r\n]+/g;
        for (; null !== (default_favicon = d.exec(response[1]));) {
          this.parse_param(default_favicon.toString(), p);
        }
        if (p.uid && !p.id) {
          p.id = p.uid;
        }
        plist.push(p);
      }
      return plist;
    }
  },
  parse_param : function(channel, events) {
    var idx = channel.indexOf(":");
    if (-1 != idx) {
      var type = channel.substr(0, idx).toLowerCase();
      var e = channel.substr(idx + 1).replace(/\\,/g, ",").replace(/[\r\n]+$/, "");
      if ("summary" == type) {
        /** @type {string} */
        type = "text";
      } else {
        if ("dtstart" == type) {
          /** @type {string} */
          type = "start_date";
          e = this.parse_date(e, 0, 0);
        } else {
          if ("dtend" == type) {
            /** @type {string} */
            type = "end_date";
            e = this.parse_date(e, 0, 0);
          }
        }
      }
      events[type] = e;
    }
  },
  parse_date : function(str, hour, minutes) {
    var chunks = str.split("T");
    if (chunks[1]) {
      hour = chunks[1].substr(0, 2);
      minutes = chunks[1].substr(2, 2);
    }
    var year = chunks[0].substr(0, 4);
    /** @type {number} */
    var month = parseInt(chunks[0].substr(4, 2), 10) - 1;
    var date = chunks[0].substr(6, 2);
    return scheduler.config.server_utc && !chunks[1] ? new Date(Date.UTC(year, month, date, hour, minutes)) : new Date(year, month, date, hour, minutes);
  },
  c_start : "BEGIN:VCALENDAR",
  e_start : "BEGIN:VEVENT",
  e_end : "END:VEVENT",
  c_end : "END:VCALENDAR"
}, scheduler._lightbox_controls = {}, scheduler.formSection = function(tagName) {
  var settings = this.config.lightbox.sections;
  /** @type {number} */
  var p = 0;
  p;
  for (; p < settings.length && settings[p].name != tagName; p++) {
  }
  var obj = settings[p];
  if (!scheduler._lightbox) {
    scheduler.getLightbox();
  }
  /** @type {(Element|null)} */
  var head = document.getElementById(obj.id);
  /** @type {(Node|null)} */
  var node = head.nextSibling;
  var params = {
    section : obj,
    header : head,
    node : node,
    getValue : function(pricePerKilo) {
      return scheduler.form_blocks[obj.type].get_value(node, pricePerKilo || {}, obj);
    },
    setValue : function(new_val, options) {
      return scheduler.form_blocks[obj.type].set_value(node, new_val, options || {}, obj);
    }
  };
  var markupFactory = scheduler._lightbox_controls["get_" + obj.type + "_control"];
  return markupFactory ? markupFactory(params) : params;
}, scheduler._lightbox_controls.get_template_control = function(scope) {
  return scope.control = scope.node, scope;
}, scheduler._lightbox_controls.get_select_control = function(api) {
  return api.control = api.node.getElementsByTagName("select")[0], api;
}, scheduler._lightbox_controls.get_textarea_control = function(api) {
  return api.control = api.node.getElementsByTagName("textarea")[0], api;
}, scheduler._lightbox_controls.get_time_control = function(item) {
  return item.control = item.node.getElementsByTagName("select"), item;
}, scheduler._lightbox_controls.defaults = {
  template : {
    height : 30
  },
  textarea : {
    height : 200
  },
  select : {
    height : 23
  },
  time : {
    height : 20
  }
}, scheduler.form_blocks = {
  template : {
    render : function(p) {
      var tpl = scheduler._lightbox_controls.defaults.template;
      var global = tpl ? tpl.height : 30;
      /** @type {string} */
      var r = (p.height || global || 30) + "px";
      return "<div class='dhx_cal_ltext dhx_cal_template' style='height:" + r + ";'></div>";
    },
    set_value : function(element, value, ev, node) {
      element.innerHTML = value || "";
    },
    get_value : function(element, context, item) {
      return element.innerHTML || "";
    },
    focus : function(bind) {
    }
  },
  textarea : {
    render : function(options) {
      var target = scheduler._lightbox_controls.defaults.textarea;
      var width = target ? target.height : 200;
      /** @type {string} */
      var r = (options.height || width || "130") + "px";
      return "<div class='dhx_cal_ltext' style='height:" + r + ";'><textarea></textarea></div>";
    },
    set_value : function(element, value, auto_add) {
      scheduler.form_blocks.textarea._get_input(element).value = value || "";
    },
    get_value : function(element, context) {
      return scheduler.form_blocks.textarea._get_input(element).value;
    },
    focus : function(e) {
      var d = scheduler.form_blocks.textarea._get_input(e);
      scheduler._focus(d, true);
    },
    _get_input : function(e) {
      return e.getElementsByTagName("textarea")[0];
    }
  },
  select : {
    render : function(options) {
      var defaults = scheduler._lightbox_controls.defaults.select;
      var height = defaults ? defaults.height : 23;
      /** @type {string} */
      var r = (options.height || height || "23") + "px";
      /** @type {string} */
      var ret = "<div class='dhx_cal_ltext' style='height:" + r + ";'><select style='width:100%;'>";
      /** @type {number} */
      var i = 0;
      for (; i < options.options.length; i++) {
        /** @type {string} */
        ret = ret + ("<option value='" + options.options[i].key + "'>" + options.options[i].label + "</option>");
      }
      return ret = ret + "</select></div>";
    },
    set_value : function(e, value, event, config) {
      var select = e.firstChild;
      if (!select._dhx_onchange && config.onchange) {
        select.onchange = config.onchange;
        /** @type {boolean} */
        select._dhx_onchange = true;
      }
      if ("undefined" == typeof value) {
        value = (select.options[0] || {}).value;
      }
      select.value = value || "";
    },
    get_value : function(element, context) {
      return element.firstChild.value;
    },
    focus : function(o) {
      var d = o.firstChild;
      scheduler._focus(d, true);
    }
  },
  time : {
    render : function(data) {
      if (!data.time_format) {
        /** @type {!Array} */
        data.time_format = ["%H:%i", "%d", "%m", "%Y"];
      }
      data._time_format_order = {};
      var f = data.time_format;
      var config = scheduler.config;
      var dt = scheduler.date.date_part(scheduler._currentDate());
      /** @type {number} */
      var d = 1440;
      /** @type {number} */
      var ContainerInstance = 0;
      if (scheduler.config.limit_time_select) {
        /** @type {number} */
        d = 60 * config.last_hour + 1;
        /** @type {number} */
        ContainerInstance = 60 * config.first_hour;
        dt.setHours(config.first_hour);
      }
      /** @type {string} */
      var pix_color = "";
      /** @type {number} */
      var i = 0;
      for (; i < f.length; i++) {
        var individual = f[i];
        if (i > 0) {
          /** @type {string} */
          pix_color = pix_color + " ";
        }
        /** @type {string} */
        var th_field = "";
        /** @type {string} */
        var summaryHtml = "";
        switch(individual) {
          case "%Y":
            /** @type {string} */
            th_field = "dhx_lightbox_year_select";
            /** @type {number} */
            data._time_format_order[3] = i;
            /** @type {number} */
            var key_5_ = dt.getFullYear() - 5;
            /** @type {number} */
            var c = 0;
            for (; 10 > c; c++) {
              /** @type {string} */
              summaryHtml = summaryHtml + ("<option value='" + (key_5_ + c) + "'>" + (key_5_ + c) + "</option>");
            }
            break;
          case "%m":
            /** @type {string} */
            th_field = "dhx_lightbox_month_select";
            /** @type {number} */
            data._time_format_order[2] = i;
            /** @type {number} */
            c = 0;
            for (; 12 > c; c++) {
              /** @type {string} */
              summaryHtml = summaryHtml + ("<option value='" + c + "'>" + this.locale.date.month_full[c] + "</option>");
            }
            break;
          case "%d":
            /** @type {string} */
            th_field = "dhx_lightbox_day_select";
            /** @type {number} */
            data._time_format_order[1] = i;
            /** @type {number} */
            c = 1;
            for (; 32 > c; c++) {
              /** @type {string} */
              summaryHtml = summaryHtml + ("<option value='" + c + "'>" + c + "</option>");
            }
            break;
          case "%H:%i":
            /** @type {string} */
            th_field = "dhx_lightbox_time_select";
            /** @type {number} */
            data._time_format_order[0] = i;
            /** @type {number} */
            c = ContainerInstance;
            var u = dt.getDate();
            /** @type {!Array} */
            data._time_values = [];
            for (; d > c;) {
              var dtitle = this.templates.time_picker(dt);
              /** @type {string} */
              summaryHtml = summaryHtml + ("<option value='" + c + "'>" + dtitle + "</option>");
              data._time_values.push(c);
              dt.setTime(dt.valueOf() + 60 * this.config.time_step * 1e3);
              /** @type {number} */
              var f = dt.getDate() != u ? 1 : 0;
              c = 24 * f * 60 + 60 * dt.getHours() + dt.getMinutes();
            }
        }
        if (summaryHtml) {
          var centraldiv = scheduler._waiAria.lightboxSelectAttrString(individual);
          /** @type {string} */
          var IDgen = data.readonly ? "disabled='disabled'" : "";
          /** @type {string} */
          pix_color = pix_color + ("<select class='" + th_field + "' " + IDgen + centraldiv + ">" + summaryHtml + "</select> ");
        }
      }
      var defaults = scheduler._lightbox_controls.defaults.select;
      var timecreated = defaults ? defaults.height : 23;
      var discTimecreated = timecreated || 30;
      return "<div style='height:" + discTimecreated + "px;padding-top:0px;font-size:inherit;' class='dhx_section_time'>" + pix_color + "<span style='font-weight:normal; font-size:10pt;'> &nbsp;&ndash;&nbsp; </span>" + pix_color + "</div>";
    },
    set_value : function(node, value, ev, config) {
      /**
       * @param {?} select
       * @param {number} data
       * @param {!Date} end
       * @return {undefined}
       */
      function update(select, data, end) {
        var crossfilterable_layers = config._time_values;
        var val = 60 * end.getHours() + end.getMinutes();
        var value = val;
        /** @type {boolean} */
        var key = false;
        /** @type {number} */
        var layer_i = 0;
        for (; layer_i < crossfilterable_layers.length; layer_i++) {
          var current = crossfilterable_layers[layer_i];
          if (current === val) {
            /** @type {boolean} */
            key = true;
            break;
          }
          if (val > current) {
            value = current;
          }
        }
        select[data + values[0]].value = key ? val : value;
        if (!(key || value)) {
          /** @type {number} */
          select[data + values[0]].selectedIndex = -1;
        }
        select[data + values[1]].value = end.getDate();
        select[data + values[2]].value = end.getMonth();
        select[data + values[3]].value = end.getFullYear();
      }
      var start_date;
      var end_date;
      var cfg = scheduler.config;
      var el = node.getElementsByTagName("select");
      var values = config._time_format_order;
      if (cfg.full_day) {
        if (!node._full_day) {
          /** @type {string} */
          var html = "<label class='dhx_fullday'><input type='checkbox' name='full_day' value='true'> " + scheduler.locale.labels.full_day + "&nbsp;</label></input>";
          if (!scheduler.config.wide_form) {
            /** @type {string} */
            html = node.previousSibling.innerHTML + html;
          }
          /** @type {string} */
          node.previousSibling.innerHTML = html;
          /** @type {boolean} */
          node._full_day = true;
        }
        var e = node.previousSibling.getElementsByTagName("input")[0];
        /** @type {boolean} */
        e.checked = 0 === scheduler.date.time_part(ev.start_date) && 0 === scheduler.date.time_part(ev.end_date);
        /** @type {boolean} */
        el[values[0]].disabled = e.checked;
        /** @type {boolean} */
        el[values[0] + el.length / 2].disabled = e.checked;
        /**
         * @return {undefined}
         */
        e.onclick = function() {
          if (e.checked) {
            var obj = {};
            scheduler.form_blocks.time.get_value(node, obj, config);
            start_date = scheduler.date.date_part(obj.start_date);
            end_date = scheduler.date.date_part(obj.end_date);
            if (+end_date == +start_date || +end_date >= +start_date && (0 !== ev.end_date.getHours() || 0 !== ev.end_date.getMinutes())) {
              end_date = scheduler.date.add(end_date, 1, "day");
            }
          } else {
            /** @type {null} */
            start_date = null;
            /** @type {null} */
            end_date = null;
          }
          el[values[0]].disabled = e.checked;
          el[values[0] + el.length / 2].disabled = e.checked;
          update(el, 0, start_date || ev.start_date);
          update(el, 4, end_date || ev.end_date);
        };
      }
      if (cfg.auto_end_date && cfg.event_duration) {
        /**
         * @return {undefined}
         */
        var _update_minical_select = function() {
          /** @type {!Date} */
          start_date = new Date(el[values[3]].value, el[values[2]].value, el[values[1]].value, 0, el[values[0]].value);
          /** @type {!Date} */
          end_date = new Date(start_date.getTime() + 60 * scheduler.config.event_duration * 1e3);
          update(el, 4, end_date);
        };
        /** @type {number} */
        var i = 0;
        for (; 4 > i; i++) {
          /** @type {function(): undefined} */
          el[i].onchange = _update_minical_select;
        }
      }
      update(el, 0, ev.start_date);
      update(el, 4, ev.end_date);
    },
    get_value : function(node, ev, v) {
      var values = node.getElementsByTagName("select");
      var args = v._time_format_order;
      if (ev.start_date = new Date(values[args[3]].value, values[args[2]].value, values[args[1]].value, 0, values[args[0]].value), ev.end_date = new Date(values[args[3] + 4].value, values[args[2] + 4].value, values[args[1] + 4].value, 0, values[args[0] + 4].value), !values[args[3]].value || !values[args[3] + 4].value) {
        var event = scheduler.getEvent(scheduler._lightbox_id);
        if (event) {
          ev.start_date = event.start_date;
          ev.end_date = event.end_date;
        }
      }
      return ev.end_date <= ev.start_date && (ev.end_date = scheduler.date.add(ev.start_date, scheduler.config.time_step, "minute")), {
        start_date : new Date(ev.start_date),
        end_date : new Date(ev.end_date)
      };
    },
    focus : function(elem) {
      scheduler._focus(elem.getElementsByTagName("select")[0]);
    }
  }
}, scheduler.showCover = function(e) {
  if (e) {
    /** @type {string} */
    e.style.display = "block";
    /** @type {number} */
    var annWidth = window.pageYOffset || document.body.scrollTop || document.documentElement.scrollTop;
    /** @type {number} */
    var annHeight = window.pageXOffset || document.body.scrollLeft || document.documentElement.scrollLeft;
    /** @type {number} */
    var pageY = window.innerHeight || document.documentElement.clientHeight;
    if (annWidth) {
      /** @type {string} */
      e.style.top = Math.round(annWidth + Math.max((pageY - e.offsetHeight) / 2, 0)) + "px";
    } else {
      /** @type {string} */
      e.style.top = Math.round(Math.max((pageY - e.offsetHeight) / 2, 0) + 9) + "px";
    }
    if (document.documentElement.scrollWidth > document.body.offsetWidth) {
      /** @type {string} */
      e.style.left = Math.round(annHeight + (document.body.offsetWidth - e.offsetWidth) / 2) + "px";
    } else {
      /** @type {string} */
      e.style.left = Math.round((document.body.offsetWidth - e.offsetWidth) / 2) + "px";
    }
  }
  this.show_cover();
}, scheduler.showLightbox = function(id) {
  if (id) {
    if (!this.callEvent("onBeforeLightbox", [id])) {
      return void(this._new_event && (this._new_event = null));
    }
    var end = this.getLightbox();
    this.showCover(end);
    this._fill_lightbox(id, end);
    this._waiAria.lightboxVisibleAttr(end);
    this.callEvent("onLightbox", [id]);
  }
}, scheduler._fill_lightbox = function(id, child) {
  var ev = this.getEvent(id);
  var enableLink = child.getElementsByTagName("span");
  /** @type {!Array} */
  var s = [];
  if (scheduler.templates.lightbox_header) {
    s.push("");
    var text = scheduler.templates.lightbox_header(ev.start_date, ev.end_date, ev);
    s.push(text);
    /** @type {string} */
    enableLink[1].innerHTML = "";
    enableLink[2].innerHTML = text;
  } else {
    var text = this.templates.event_header(ev.start_date, ev.end_date, ev);
    var d = (this.templates.event_bar_text(ev.start_date, ev.end_date, ev) || "").substr(0, 70);
    s.push(text);
    s.push(d);
    enableLink[1].innerHTML = text;
    enableLink[2].innerHTML = d;
  }
  this._waiAria.lightboxHeader(child, s.join(" "));
  var children = this.config.lightbox.sections;
  /** @type {number} */
  var j = 0;
  for (; j < children.length; j++) {
    var config = children[j];
    var superConfig = scheduler._get_lightbox_section_node(config);
    var widget = this.form_blocks[config.type];
    var throw42 = void 0 !== ev[config.map_to] ? ev[config.map_to] : config.default_value;
    widget.set_value.call(this, superConfig, throw42, ev, config);
    if (children[j].focus) {
      widget.focus.call(this, superConfig);
    }
  }
  /** @type {string} */
  scheduler._lightbox_id = id;
}, scheduler._get_lightbox_section_node = function(o) {
  return document.getElementById(o.id).nextSibling;
}, scheduler._lightbox_out = function(event_data) {
  var source = this.config.lightbox.sections;
  /** @type {number} */
  var i = 0;
  for (; i < source.length; i++) {
    /** @type {(Element|null)} */
    var child = document.getElementById(source[i].id);
    /** @type {(Node|null)} */
    child = child ? child.nextSibling : child;
    var settings = this.form_blocks[source[i].type];
    var alignContentAlignItem = settings.get_value.call(this, child, event_data, source[i]);
    if ("auto" != source[i].map_to) {
      event_data[source[i].map_to] = alignContentAlignItem;
    }
  }
  return event_data;
}, scheduler._empty_lightbox = function(x) {
  var t = scheduler._lightbox_id;
  var e = this.getEvent(t);
  this.getLightbox();
  this._lame_copy(e, x);
  this.setEvent(e.id, e);
  this._edit_stop_event(e, true);
  this.render_view_data();
}, scheduler.hide_lightbox = function(canCreateDiscussions) {
  scheduler.endLightbox(false, this.getLightbox());
}, scheduler.hideCover = function(editor) {
  if (editor) {
    /** @type {string} */
    editor.style.display = "none";
  }
  this.hide_cover();
}, scheduler.hide_cover = function() {
  if (this._cover) {
    this._cover.parentNode.removeChild(this._cover);
  }
  /** @type {null} */
  this._cover = null;
}, scheduler.show_cover = function() {
  if (!this._cover) {
    /** @type {!Element} */
    this._cover = document.createElement("div");
    /** @type {string} */
    this._cover.className = "dhx_cal_cover";
    /** @type {number} */
    var minEditorHieght = void 0 !== document.height ? document.height : document.body.offsetHeight;
    /** @type {number} */
    var minimumSpace = document.documentElement ? document.documentElement.scrollHeight : 0;
    /** @type {string} */
    this._cover.style.height = Math.max(minEditorHieght, minimumSpace) + "px";
    document.body.appendChild(this._cover);
  }
}, scheduler.save_lightbox = function() {
  var tInd = this._lightbox_out({}, this._lame_copy(this.getEvent(this._lightbox_id)));
  if (!this.checkEvent("onEventSave") || this.callEvent("onEventSave", [this._lightbox_id, tInd, this._new_event])) {
    this._empty_lightbox(tInd);
    this.hide_lightbox();
  }
}, scheduler.startLightbox = function(s, prefix) {
  /** @type {string} */
  this._lightbox_id = s;
  /** @type {boolean} */
  this._custom_lightbox = true;
  this._temp_lightbox = this._lightbox;
  /** @type {!Element} */
  this._lightbox = prefix;
  this.showCover(prefix);
}, scheduler.endLightbox = function(mode, password) {
  password = password || scheduler.getLightbox();
  var $noRangeMsg = scheduler.getEvent(this._lightbox_id);
  if ($noRangeMsg) {
    this._edit_stop_event($noRangeMsg, mode);
  }
  if (mode) {
    scheduler.render_view_data();
  }
  this.hideCover(password);
  if (this._custom_lightbox) {
    this._lightbox = this._temp_lightbox;
    /** @type {boolean} */
    this._custom_lightbox = false;
  }
  /** @type {null} */
  this._temp_lightbox = this._lightbox_id = null;
  this._waiAria.lightboxHiddenAttr(password);
  this.callEvent("onAfterLightbox", []);
}, scheduler.resetLightbox = function() {
  if (scheduler._lightbox && !scheduler._custom_lightbox) {
    scheduler._lightbox.parentNode.removeChild(scheduler._lightbox);
  }
  /** @type {null} */
  scheduler._lightbox = null;
}, scheduler.cancel_lightbox = function() {
  this.callEvent("onEventCancel", [this._lightbox_id, this._new_event]);
  this.hide_lightbox();
}, scheduler._init_lightbox_events = function() {
  /**
   * @param {!Function} ev
   * @return {undefined}
   */
  this.getLightbox().onclick = function(ev) {
    var item = ev ? ev.target : event.srcElement;
    if (item.className || (item = item.previousSibling), !(item && item.className && scheduler._getClassName(item).indexOf("dhx_btn_set") > -1) || (item = item.querySelector("[dhx_button]"))) {
      var copy = scheduler._getClassName(item);
      if (item && copy) {
        switch(copy) {
          case "dhx_save_btn":
            scheduler.save_lightbox();
            break;
          case "dhx_delete_btn":
            var temp = scheduler.locale.labels.confirm_deleting;
            scheduler._dhtmlx_confirm(temp, scheduler.locale.labels.title_confirm_deleting, function() {
              scheduler.deleteEvent(scheduler._lightbox_id);
              /** @type {null} */
              scheduler._new_event = null;
              scheduler.hide_lightbox();
            });
            break;
          case "dhx_cancel_btn":
            scheduler.cancel_lightbox();
            break;
          default:
            if (item.getAttribute("dhx_button")) {
              scheduler.callEvent("onLightboxButton", [copy, item, ev]);
            } else {
              var name;
              var e;
              var f;
              if (-1 != copy.indexOf("dhx_custom_button")) {
                if (-1 != copy.indexOf("dhx_custom_button_")) {
                  name = item.parentNode.getAttribute("index");
                  f = item.parentNode.parentNode;
                } else {
                  name = item.getAttribute("index");
                  f = item.parentNode;
                  item = item.firstChild;
                }
              }
              if (name) {
                e = scheduler.form_blocks[scheduler.config.lightbox.sections[name].type];
                e.button_click(name, item, f, f.nextSibling);
              }
            }
        }
      }
    }
  };
  /**
   * @param {!Object} e
   * @return {undefined}
   */
  this.getLightbox().onkeydown = function(e) {
    var event = e || window.event;
    var editheader = e.target || e.srcElement;
    var events = editheader.querySelector("[dhx_button]");
    switch(events || (events = editheader.parentNode.querySelector(".dhx_custom_button, .dhx_readonly")), (e || event).keyCode) {
      case 32:
        if ((e || event).shiftKey) {
          return;
        }
        if (events && events.click) {
          events.click();
        }
        break;
      case scheduler.keys.edit_save:
        if ((e || event).shiftKey) {
          return;
        }
        if (events && events.click) {
          events.click();
        } else {
          scheduler.save_lightbox();
        }
        break;
      case scheduler.keys.edit_cancel:
        scheduler.cancel_lightbox();
    }
  };
}, scheduler.setLightboxSize = function() {
  var e = this._lightbox;
  if (e) {
    var focusedTextBox = e.childNodes[1];
    /** @type {string} */
    focusedTextBox.style.height = "0px";
    /** @type {string} */
    focusedTextBox.style.height = focusedTextBox.scrollHeight + "px";
    /** @type {string} */
    e.style.height = focusedTextBox.scrollHeight + scheduler.xy.lightbox_additional_height + "px";
    /** @type {string} */
    focusedTextBox.style.height = focusedTextBox.scrollHeight + "px";
  }
}, scheduler._init_dnd_events = function() {
  dhtmlxEvent(document.body, "mousemove", scheduler._move_while_dnd);
  dhtmlxEvent(document.body, "mouseup", scheduler._finish_dnd);
  /**
   * @return {undefined}
   */
  scheduler._init_dnd_events = function() {
  };
}, scheduler._move_while_dnd = function(touch) {
  if (scheduler._dnd_start_lb) {
    if (!document.dhx_unselectable) {
      document.body.className += " dhx_unselectable";
      /** @type {boolean} */
      document.dhx_unselectable = true;
    }
    var swipeDiv = scheduler.getLightbox();
    /** @type {!Array} */
    var i = touch && touch.target ? [touch.pageX, touch.pageY] : [event.clientX, event.clientY];
    /** @type {string} */
    swipeDiv.style.top = scheduler._lb_start[1] + i[1] - scheduler._dnd_start_lb[1] + "px";
    /** @type {string} */
    swipeDiv.style.left = scheduler._lb_start[0] + i[0] - scheduler._dnd_start_lb[0] + "px";
  }
}, scheduler._ready_to_dnd = function(e) {
  var swipeDiv = scheduler.getLightbox();
  /** @type {!Array} */
  scheduler._lb_start = [parseInt(swipeDiv.style.left, 10), parseInt(swipeDiv.style.top, 10)];
  /** @type {!Array} */
  scheduler._dnd_start_lb = e && e.target ? [e.pageX, e.pageY] : [event.clientX, event.clientY];
}, scheduler._finish_dnd = function() {
  if (scheduler._lb_start) {
    /** @type {boolean} */
    scheduler._lb_start = scheduler._dnd_start_lb = false;
    /** @type {string} */
    document.body.className = document.body.className.replace(" dhx_unselectable", "");
    /** @type {boolean} */
    document.dhx_unselectable = false;
  }
}, scheduler.getLightbox = function() {
  if (!this._lightbox) {
    /** @type {!Element} */
    var p = document.createElement("div");
    /** @type {string} */
    p.className = "dhx_cal_light";
    if (scheduler.config.wide_form) {
      p.className += " dhx_cal_light_wide";
    }
    if (scheduler.form_blocks.recurring) {
      p.className += " dhx_cal_light_rec";
    }
    if (/msie|MSIE 6/.test(navigator.userAgent)) {
      p.className += " dhx_ie6";
    }
    /** @type {string} */
    p.style.visibility = "hidden";
    var html = this._lightbox_template;
    var id = this.config.buttons_left;
    /** @type {string} */
    var th_field = "";
    /** @type {number} */
    var i = 0;
    for (; i < id.length; i++) {
      th_field = this._waiAria.lightboxButtonAttrString(id[i]);
      /** @type {string} */
      html = html + ("<div " + th_field + " class='dhx_btn_set dhx_left_btn_set " + id[i] + "_set'><div dhx_button='1' class='" + id[i] + "'></div><div>" + scheduler.locale.labels[id[i]] + "</div></div>");
    }
    id = this.config.buttons_right;
    /** @type {number} */
    i = 0;
    for (; i < id.length; i++) {
      th_field = this._waiAria.lightboxButtonAttrString(id[i]);
      /** @type {string} */
      html = html + ("<div " + th_field + " class='dhx_btn_set dhx_right_btn_set " + id[i] + "_set' style='float:right;'><div dhx_button='1' class='" + id[i] + "'></div><div>" + scheduler.locale.labels[id[i]] + "</div></div>");
    }
    /** @type {string} */
    html = html + "</div>";
    /** @type {string} */
    p.innerHTML = html;
    if (scheduler.config.drag_lightbox) {
      /** @type {function(!Object): undefined} */
      p.firstChild.onmousedown = scheduler._ready_to_dnd;
      /**
       * @return {?}
       */
      p.firstChild.onselectstart = function() {
        return false;
      };
      /** @type {string} */
      p.firstChild.style.cursor = "move";
      scheduler._init_dnd_events();
    }
    this._waiAria.lightboxAttr(p);
    document.body.insertBefore(p, document.body.firstChild);
    /** @type {!Element} */
    this._lightbox = p;
    var buttons = this.config.lightbox.sections;
    /** @type {string} */
    html = "";
    /** @type {number} */
    i = 0;
    for (; i < buttons.length; i++) {
      var n = this.form_blocks[buttons[i].type];
      if (n) {
        buttons[i].id = "area_" + this.uid();
        /** @type {string} */
        var patch3c = "";
        if (buttons[i].button) {
          th_field = scheduler._waiAria.lightboxSectionButtonAttrString(this.locale.labels["button_" + buttons[i].button]);
          /** @type {string} */
          patch3c = "<div " + th_field + " class='dhx_custom_button' index='" + i + "'><div class='dhx_custom_button_" + buttons[i].button + "'></div><div>" + this.locale.labels["button_" + buttons[i].button] + "</div></div>";
        }
        if (this.config.wide_form) {
          /** @type {string} */
          html = html + "<div class='dhx_wrap_section'>";
        }
        var table = this.locale.labels["section_" + buttons[i].name];
        if ("string" != typeof table) {
          table = buttons[i].name;
        }
        /** @type {string} */
        html = html + ("<div id='" + buttons[i].id + "' class='dhx_cal_lsection'>" + patch3c + "<label>" + table + "</label></div>" + n.render.call(this, buttons[i]));
        /** @type {string} */
        html = html + "</div>";
      }
    }
    /** @type {!NodeList<Element>} */
    var elms = p.getElementsByTagName("div");
    /** @type {number} */
    i = 0;
    for (; i < elms.length; i++) {
      /** @type {!Element} */
      var e = elms[i];
      var eNeg = scheduler._getClassName(e);
      if ("dhx_cal_larea" == eNeg) {
        /** @type {string} */
        e.innerHTML = html;
        break;
      }
    }
    scheduler._bindLightboxLabels(buttons);
    this.setLightboxSize();
    this._init_lightbox_events(this);
    /** @type {string} */
    p.style.display = "none";
    /** @type {string} */
    p.style.visibility = "visible";
  }
  return this._lightbox;
}, scheduler._bindLightboxLabels = function(ary) {
  /** @type {number} */
  var i = 0;
  for (; i < ary.length; i++) {
    var obj = ary[i];
    if (obj.id && document.getElementById(obj.id)) {
      /** @type {(Element|null)} */
      var r = document.getElementById(obj.id);
      /** @type {(Element|null)} */
      var node = r.querySelector("label");
      var n = scheduler._get_lightbox_section_node(obj);
      for (; n && !n.querySelector;) {
        n = n.nextSibling;
      }
      /** @type {boolean} */
      var a = true;
      if (n) {
        var tooltipObj = n.querySelector("input, select, textarea");
        if (tooltipObj) {
          obj.inputId = tooltipObj.id || "input_" + scheduler.uid();
          if (!tooltipObj.id) {
            tooltipObj.id = obj.inputId;
          }
          node.setAttribute("for", obj.inputId);
          /** @type {boolean} */
          a = false;
        }
      }
      if (a) {
        var inlineEditor2 = scheduler.form_blocks[obj.type];
        if (inlineEditor2.focus) {
          node.onclick = function(obj) {
            return function() {
              var widget = scheduler.form_blocks[obj.type];
              var objBackup = scheduler._get_lightbox_section_node(obj);
              if (widget && widget.focus) {
                widget.focus.call(scheduler, objBackup);
              }
            };
          }(obj);
        }
      }
    }
  }
}, scheduler.attachEvent("onEventIdChange", function(canCreateDiscussions, isSlidingUp) {
  if (this._lightbox_id == canCreateDiscussions) {
    /** @type {string} */
    this._lightbox_id = isSlidingUp;
  }
}), scheduler._lightbox_template = "<div class='dhx_cal_ltitle'><span class='dhx_mark'>&nbsp;</span><span class='dhx_time'></span><span class='dhx_title'></span></div><div class='dhx_cal_larea'></div>", scheduler._init_touch_events = function() {
  var e = this.config.touch && (-1 != navigator.userAgent.indexOf("Mobile") || -1 != navigator.userAgent.indexOf("iPad") || -1 != navigator.userAgent.indexOf("Android") || -1 != navigator.userAgent.indexOf("Touch")) && !window.MSStream;
  if (e && (this.xy.scroll_width = 0, this._mobile = true), this.config.touch) {
    /** @type {boolean} */
    var t = true;
    try {
      document.createEvent("TouchEvent");
    } catch (i) {
      /** @type {boolean} */
      t = false;
    }
    if (t) {
      this._touch_events(["touchmove", "touchstart", "touchend"], function(event) {
        return event.touches && event.touches.length > 1 ? null : event.touches[0] ? {
          target : event.target,
          pageX : event.touches[0].pageX,
          pageY : event.touches[0].pageY,
          clientX : event.touches[0].clientX,
          clientY : event.touches[0].clientY
        } : event;
      }, function() {
        return false;
      });
    } else {
      if (window.PointerEvent || window.navigator.pointerEnabled) {
        this._touch_events(["pointermove", "pointerdown", "pointerup"], function(event) {
          return "mouse" == event.pointerType ? null : event;
        }, function(event) {
          return !event || "mouse" == event.pointerType;
        });
      } else {
        if (window.navigator.msPointerEnabled) {
          this._touch_events(["MSPointerMove", "MSPointerDown", "MSPointerUp"], function(e) {
            return e.pointerType == e.MSPOINTER_TYPE_MOUSE ? null : e;
          }, function(e) {
            return !e || e.pointerType == e.MSPOINTER_TYPE_MOUSE;
          });
        }
      }
    }
  }
}, scheduler._touch_events = function(obj, func, isArray) {
  /**
   * @param {!Object} window
   * @param {string} type
   * @param {!Function} next
   * @return {undefined}
   */
  function init(window, type, next) {
    window.addEventListener(type, function(b) {
      if (scheduler._is_lightbox_open()) {
        return true;
      }
      if (!isArray(b)) {
        return next(b);
      }
    }, {
      passive : false
    });
  }
  /**
   * @param {!Event} e
   * @param {!MouseEvent} pos
   * @param {number} scale
   * @param {number} time
   * @return {?}
   */
  function render(e, pos, scale, time) {
    if (!e || !pos) {
      return false;
    }
    var node = e.target;
    for (; node && node != scheduler._obj;) {
      node = node.parentNode;
    }
    if (node != scheduler._obj) {
      return false;
    }
    if (scheduler.matrix && scheduler.matrix[scheduler.getState().mode]) {
      var swiper = scheduler.matrix[scheduler.getState().mode];
      if (swiper.scrollable) {
        return false;
      }
    }
    /** @type {number} */
    var length = Math.abs(e.pageY - pos.pageY);
    /** @type {number} */
    var x = Math.abs(e.pageX - pos.pageX);
    return time > length && x > scale && (!length || x / length > 3) ? (e.pageX > pos.pageX ? scheduler._click.dhx_cal_next_button() : scheduler._click.dhx_cal_prev_button(), true) : false;
  }
  /**
   * @param {!Event} e
   * @return {?}
   */
  function listener(e) {
    if (!isArray(e)) {
      var name = scheduler.getState().drag_mode;
      var value = scheduler.matrix ? scheduler.matrix[scheduler._mode] : false;
      /** @type {function(!Array, string): ?} */
      var select_id = scheduler.render_view_data;
      return "create" == name && value && (scheduler.render_view_data = function() {
        var event_id = scheduler.getState().drag_id;
        var ev = scheduler.getEvent(event_id);
        var j = value.y_property;
        var stack = scheduler.getEvents(ev.start_date, ev.end_date);
        /** @type {number} */
        var i = 0;
        for (; i < stack.length; i++) {
          if (stack[i][j] != ev[j]) {
            stack.splice(i, 1);
            i--;
          }
        }
        /** @type {number} */
        ev._sorder = stack.length - 1;
        ev._count = stack.length;
        this.render_data([ev], scheduler.getState().mode);
      }), scheduler._on_mouse_move(e), "create" == name && value && (scheduler.render_view_data = select_id), e.preventDefault && e.preventDefault(), e.cancelBubble = true, false;
    }
  }
  /**
   * @param {boolean} e
   * @return {undefined}
   */
  function next(e) {
    if (!isArray(e)) {
      scheduler._hide_global_tip();
      if (use_cycle_mode) {
        scheduler._on_mouse_up(func(e || event));
        /** @type {boolean} */
        scheduler._temp_touch_block = false;
      }
      /** @type {null} */
      scheduler._drag_id = null;
      /** @type {null} */
      scheduler._drag_mode = null;
      /** @type {null} */
      scheduler._drag_pos = null;
      /** @type {null} */
      scheduler._pointerDragId = null;
      clearTimeout(t);
      /** @type {boolean} */
      use_cycle_mode = deep = false;
      /** @type {boolean} */
      o = true;
    }
  }
  var evt;
  var data;
  var t;
  var use_cycle_mode;
  var o;
  var deep;
  /** @type {number} */
  var gestureThrottle = (-1 != navigator.userAgent.indexOf("Android") && -1 != navigator.userAgent.indexOf("WebKit"), 0);
  init(document.body, obj[0], function(event) {
    if (!isArray(event)) {
      var value = func(event);
      if (value) {
        if (use_cycle_mode) {
          return listener(value), event.preventDefault && event.preventDefault(), event.cancelBubble = true, scheduler._update_global_tip(), false;
        }
        if (data = func(event), deep) {
          return data ? void((evt.target != data.target || Math.abs(evt.pageX - data.pageX) > 5 || Math.abs(evt.pageY - data.pageY) > 5) && (o = true, clearTimeout(t))) : void(o = true);
        }
      }
    }
  });
  init(this._els.dhx_cal_data[0], "touchcancel", next);
  init(this._els.dhx_cal_data[0], "contextmenu", function(e) {
    return isArray(e) ? void 0 : deep ? (e && e.preventDefault && e.preventDefault(), (e || event).cancelBubble = true, false) : void 0;
  });
  init(this._obj, obj[1], function(event) {
    if (!isArray(event)) {
      scheduler._pointerDragId = event.pointerId;
      var ev;
      if (use_cycle_mode = o = false, deep = true, ev = data = func(event), !ev) {
        return void(o = true);
      }
      /** @type {!Date} */
      var d = new Date;
      if (!o && !use_cycle_mode && 250 > d - gestureThrottle) {
        return scheduler._click.dhx_cal_data(ev), window.setTimeout(function() {
          /** @type {string} */
          ev.type = "dblclick";
          scheduler._on_dbl_click(ev);
        }, 50), event.preventDefault && event.preventDefault(), event.cancelBubble = true, scheduler._block_next_stop = true, false;
      }
      if (gestureThrottle = d, !o && !use_cycle_mode && scheduler.config.touch_drag) {
        var a = scheduler._locate_event(document.activeElement);
        var b = scheduler._locate_event(ev.target);
        var aP = evt ? scheduler._locate_event(evt.target) : null;
        if (a && b && a == b && a != aP) {
          return event.preventDefault && event.preventDefault(), event.cancelBubble = true, scheduler._ignore_next_click = false, scheduler._click.dhx_cal_data(ev), evt = ev, false;
        }
        /** @type {number} */
        t = setTimeout(function() {
          /** @type {boolean} */
          use_cycle_mode = true;
          var e = evt.target;
          var se1 = scheduler._getClassName(e);
          if (e && -1 != se1.indexOf("dhx_body")) {
            e = e.previousSibling;
          }
          scheduler._on_mouse_down(evt, e);
          if (scheduler._drag_mode && "create" != scheduler._drag_mode) {
            scheduler.for_rendered(scheduler._drag_id, function(builderID, idxC) {
              /** @type {string} */
              builderID.style.display = "none";
              scheduler._rendered.splice(idxC, 1);
            });
          }
          if (scheduler.config.touch_tip) {
            scheduler._show_global_tip();
          }
          scheduler.updateEvent(scheduler._drag_id);
        }, scheduler.config.touch_drag);
        evt = ev;
      }
    }
  });
  init(this._els.dhx_cal_data[0], obj[2], function(e) {
    return isArray(e) ? void 0 : (!use_cycle_mode && render(evt, data, 200, 100) && (scheduler._block_next_stop = true), use_cycle_mode && (scheduler._ignore_next_click = true, setTimeout(function() {
      /** @type {boolean} */
      scheduler._ignore_next_click = false;
    }, 100)), next(e), scheduler._block_next_stop ? (scheduler._block_next_stop = false, e.preventDefault && e.preventDefault(), e.cancelBubble = true, false) : void 0);
  });
  dhtmlxEvent(document.body, obj[2], next);
}, scheduler._show_global_tip = function() {
  scheduler._hide_global_tip();
  /** @type {!Element} */
  var whiteBox = scheduler._global_tip = document.createElement("div");
  /** @type {string} */
  whiteBox.className = "dhx_global_tip";
  scheduler._update_global_tip(1);
  document.body.appendChild(whiteBox);
}, scheduler._update_global_tip = function(zoomAware) {
  var box = scheduler._global_tip;
  if (box) {
    /** @type {string} */
    var body = "";
    if (scheduler._drag_id && !zoomAware) {
      var ev = scheduler.getEvent(scheduler._drag_id);
      if (ev) {
        /** @type {string} */
        body = "<div>" + (ev._timed ? scheduler.templates.event_header(ev.start_date, ev.end_date, ev) : scheduler.templates.day_date(ev.start_date, ev.end_date, ev)) + "</div>";
      }
    }
    if ("create" == scheduler._drag_mode || "new-size" == scheduler._drag_mode) {
      /** @type {string} */
      box.innerHTML = (scheduler.locale.labels.drag_to_create || "Drag to create") + body;
    } else {
      /** @type {string} */
      box.innerHTML = (scheduler.locale.labels.drag_to_move || "Drag to move") + body;
    }
  }
}, scheduler._hide_global_tip = function() {
  var t = scheduler._global_tip;
  if (t && t.parentNode) {
    t.parentNode.removeChild(t);
    /** @type {number} */
    scheduler._global_tip = 0;
  }
}, scheduler._dp_init = function(self) {
  /** @type {!Array} */
  self._methods = ["_set_event_text_style", "", "_dp_change_event_id", "_dp_hook_delete"];
  /**
   * @param {undefined} event_id
   * @param {string} day
   * @return {undefined}
   */
  this._dp_change_event_id = function(event_id, day) {
    if (scheduler.getEvent(event_id)) {
      scheduler.changeEventId(event_id, day);
    }
  };
  /**
   * @param {undefined} id
   * @param {!Object} rowId
   * @return {?}
   */
  this._dp_hook_delete = function(id, rowId) {
    return scheduler.getEvent(id) ? (rowId && id != rowId && ("true_deleted" == this.getUserData(id, self.action_param) && this.setUserData(id, self.action_param, "updated"), this.changeEventId(id, rowId)), this.deleteEvent(rowId, true)) : void 0;
  };
  this.attachEvent("onEventAdded", function(id) {
    if (!this._loading && this._validId(id)) {
      self.setUpdated(id, true, "inserted");
    }
  });
  this.attachEvent("onConfirmedBeforeEventDelete", function(id) {
    if (this._validId(id)) {
      var type = self.getState(id);
      return "inserted" == type || this._new_event ? (self.setUpdated(id, false), true) : "deleted" == type ? false : "true_deleted" == type ? true : (self.setUpdated(id, true, "deleted"), false);
    }
  });
  this.attachEvent("onEventChanged", function(id) {
    if (!this._loading && this._validId(id)) {
      self.setUpdated(id, true, "updated");
    }
  });
  scheduler.attachEvent("onClearAll", function() {
    self._in_progress = {};
    self._invalid = {};
    /** @type {!Array} */
    self.updatedRows = [];
    /** @type {number} */
    self._waitMode = 0;
  });
  /**
   * @param {!Object} obj
   * @param {!Object} f
   * @param {string} c
   * @return {?}
   */
  self._objToJson = function(obj, f, c) {
    c = c || "";
    f = f || {};
    var i;
    for (i in obj) {
      if (0 !== i.indexOf("_")) {
        if (obj[i] && obj[i].getUTCFullYear) {
          f[c + i] = this.obj.templates.xml_format(obj[i]);
        } else {
          if (obj[i] && "object" == typeof obj[i]) {
            self._objToJson(obj[i], f, c + i + ".");
          } else {
            f[c + i] = obj[i];
          }
        }
      }
    }
    return f;
  };
  /**
   * @param {!Array} key
   * @param {?} index
   * @return {?}
   */
  self._getRowData = function(key, index) {
    var metricStats = this.obj.getEvent(key);
    return this._objToJson(metricStats);
  };
  /**
   * @return {undefined}
   */
  self._clearUpdateFlag = function() {
  };
  self.attachEvent("insertCallback", scheduler._update_callback);
  self.attachEvent("updateCallback", scheduler._update_callback);
  self.attachEvent("deleteCallback", function(key, id) {
    if (this.obj.getEvent(id)) {
      this.obj.setUserData(id, this.action_param, "true_deleted");
      this.obj.deleteEvent(id);
    } else {
      if (this.obj._add_rec_marker) {
        this.obj._update_callback(key, id);
      }
    }
  });
}, scheduler._validId = function(studentId) {
  return true;
}, scheduler.setUserData = function(id, name, value) {
  if (id) {
    var event = this.getEvent(id);
    if (event) {
      /** @type {string} */
      event[name] = value;
    }
  } else {
    /** @type {string} */
    this._userdata[name] = value;
  }
}, scheduler.getUserData = function(id, name) {
  if (id) {
    var result = this.getEvent(id);
    return result ? result[name] : null;
  }
  return this._userdata[name];
}, scheduler._set_event_text_style = function(event_id, value) {
  if (scheduler.getEvent(event_id)) {
    this.for_rendered(event_id, function(switchButton) {
      switchButton.style.cssText += ";" + value;
    });
    var ev = this.getEvent(event_id);
    /** @type {string} */
    ev._text_style = value;
    this.event_updated(ev);
  }
}, scheduler._update_callback = function(node, context) {
  var event = scheduler._xmlNodeToJSON(node.firstChild);
  if ("none" == event.rec_type) {
    /** @type {string} */
    event.rec_pattern = "none";
  }
  event.text = event.text || event._tagvalue;
  event.start_date = scheduler.templates.xml_date(event.start_date);
  event.end_date = scheduler.templates.xml_date(event.end_date);
  scheduler.addEvent(event);
  if (scheduler._add_rec_marker) {
    scheduler.setCurrentView();
  }
}, scheduler._skin_settings = {
  fix_tab_position : [1, 0],
  use_select_menu_space : [1, 0],
  wide_form : [1, 0],
  hour_size_px : [44, 42],
  displayed_event_color : ["#ff4a4a", "ffc5ab"],
  displayed_event_text_color : ["#ffef80", "7e2727"]
}, scheduler._skin_xy = {
  lightbox_additional_height : [90, 50],
  nav_height : [59, 22],
  bar_height : [24, 20]
}, scheduler._is_material_skin = function() {
  return (scheduler.skin + "").indexOf("material") > -1;
}, scheduler._border_box_bvents = function() {
  return scheduler._is_material_skin();
}, scheduler._configure = function(options, facet, i) {
  var type;
  for (type in facet) {
    if ("undefined" == typeof options[type]) {
      options[type] = facet[type][i];
    }
  }
}, scheduler._skin_init = function() {
  if (!scheduler.skin) {
    /** @type {!NodeList<Element>} */
    var cssStyles = document.getElementsByTagName("link");
    /** @type {number} */
    var i = 0;
    for (; i < cssStyles.length; i++) {
      var skins = cssStyles[i].href.match("dhtmlxscheduler_([a-z]+).css");
      if (skins) {
        scheduler.skin = skins[1];
        break;
      }
    }
  }
  /** @type {number} */
  var NINETY_EIGHT_HOURS = 0;
  if (!scheduler.skin || "classic" !== scheduler.skin && "glossy" !== scheduler.skin || (NINETY_EIGHT_HOURS = 1), scheduler._is_material_skin()) {
    var b = scheduler.config.buttons_left.$inital;
    var a = scheduler.config.buttons_right.$inital;
    if (b && scheduler.config.buttons_left.slice().join() == b && a && scheduler.config.buttons_right.slice().join() == a) {
      var n = scheduler.config.buttons_left.slice();
      scheduler.config.buttons_left = scheduler.config.buttons_right.slice();
      scheduler.config.buttons_right = n;
    }
    /** @type {number} */
    scheduler.xy.event_header_height = 18;
    /** @type {number} */
    scheduler.xy.menu_width = 25;
    /** @type {number} */
    scheduler.xy.week_agenda_scale_height = 35;
    /** @type {number} */
    scheduler.xy.map_icon_width = 38;
    /** @type {number} */
    scheduler._lightbox_controls.defaults.textarea.height = 64;
    /** @type {string} */
    scheduler._lightbox_controls.defaults.time.height = "auto";
  }
  if (this._configure(scheduler.config, scheduler._skin_settings, NINETY_EIGHT_HOURS), this._configure(scheduler.xy, scheduler._skin_xy, NINETY_EIGHT_HOURS), "flat" === scheduler.skin && (scheduler.xy.scale_height = 35, scheduler.templates.hour_scale = function(def) {
    var min = def.getMinutes();
    min = 10 > min ? "0" + min : min;
    /** @type {string} */
    var i = "<span class='dhx_scale_h'>" + def.getHours() + "</span><span class='dhx_scale_m'>&nbsp;" + min + "</span>";
    return i;
  }), !NINETY_EIGHT_HOURS) {
    var nonOverlappingLayout = scheduler.config.minicalendar;
    if (nonOverlappingLayout) {
      /** @type {number} */
      nonOverlappingLayout.padding = 14;
    }
    /**
     * @param {?} start
     * @param {?} end
     * @param {!Object} ev
     * @return {?}
     */
    scheduler.templates.event_bar_date = function(start, end, ev) {
      return "\u2022 <b>" + scheduler.templates.event_date(start) + "</b> ";
    };
    scheduler.attachEvent("onTemplatesReady", function() {
      var date_to_str = scheduler.date.date_to_str("%d");
      if (!scheduler.templates._old_month_day) {
        scheduler.templates._old_month_day = scheduler.templates.month_day;
      }
      var onExternalDropEvent = scheduler.templates._old_month_day;
      if (scheduler.templates.month_day = function(date) {
        if ("month" == this._mode) {
          var label = date_to_str(date);
          return 1 == date.getDate() && (label = scheduler.locale.date.month_full[date.getMonth()] + " " + label), +date == +scheduler.date.date_part(this._currentDate()) && (label = scheduler.locale.labels.dhx_cal_today_button + " " + label), label;
        }
        return onExternalDropEvent.call(this, date);
      }, scheduler.config.fix_tab_position) {
        var inputs = scheduler._els.dhx_cal_navline[0].getElementsByTagName("div");
        /** @type {null} */
        var tooltipEl = null;
        /** @type {number} */
        var left = 211;
        /** @type {!Array} */
        var absoluteMousePos = [14, 75, 136];
        /** @type {number} */
        var x = 14;
        if (scheduler._is_material_skin()) {
          /** @type {!Array} */
          absoluteMousePos = [16, 103, 192];
          /** @type {number} */
          left = 294;
          /** @type {number} */
          x = -1;
        }
        /** @type {number} */
        var i = 0;
        for (; i < inputs.length; i++) {
          var el = inputs[i];
          var name = el.getAttribute("name");
          if (name) {
            switch(el.style.right = "auto", name) {
              case "day_tab":
                /** @type {string} */
                el.style.left = absoluteMousePos[0] + "px";
                el.className += " dhx_cal_tab_first";
                break;
              case "week_tab":
                /** @type {string} */
                el.style.left = absoluteMousePos[1] + "px";
                break;
              case "month_tab":
                /** @type {string} */
                el.style.left = absoluteMousePos[2] + "px";
                el.className += " dhx_cal_tab_last";
                break;
              default:
                /** @type {string} */
                el.style.left = left + "px";
                el.className += " dhx_cal_tab_standalone";
                left = left + x + el.offsetWidth;
            }
            el.className += " " + name;
          } else {
            if (0 === (el.className || "").indexOf("dhx_minical_icon") && el.parentNode == scheduler._els.dhx_cal_navline[0]) {
              tooltipEl = el;
            }
          }
        }
        if (tooltipEl) {
          /** @type {string} */
          tooltipEl.style.left = left + "px";
        }
      }
    });
    /**
     * @return {undefined}
     */
    scheduler._skin_init = function() {
    };
  }
}, window.jQuery && !function($) {
  /** @type {!Array} */
  var t = [];
  /**
   * @param {string} value
   * @return {?}
   */
  $.fn.dhx_scheduler = function(value) {
    if ("string" != typeof value) {
      /** @type {!Array} */
      var xs = [];
      return this.each(function() {
        if (this && this.getAttribute && !this.getAttribute("dhxscheduler")) {
          var id;
          for (id in value) {
            if ("data" != id) {
              scheduler.config[id] = value[id];
            }
          }
          if (!this.getElementsByTagName("div").length) {
            /** @type {string} */
            this.innerHTML = '<div class="dhx_cal_navline"><div class="dhx_cal_prev_button">&nbsp;</div><div class="dhx_cal_next_button">&nbsp;</div><div class="dhx_cal_today_button"></div><div class="dhx_cal_date"></div><div class="dhx_cal_tab" name="day_tab" style="right:204px;"></div><div class="dhx_cal_tab" name="week_tab" style="right:140px;"></div><div class="dhx_cal_tab" name="month_tab" style="right:76px;"></div></div><div class="dhx_cal_header"></div><div class="dhx_cal_data"></div>';
            this.className += " dhx_cal_container";
          }
          scheduler.init(this, scheduler.config.date, scheduler.config.mode);
          if (value.data) {
            scheduler.parse(value.data);
          }
          xs.push(scheduler);
        }
      }), 1 === xs.length ? xs[0] : xs;
    }
    return t[value] ? t[value].apply(this, []) : void $.error("Method " + value + " does not exist on jQuery.dhx_scheduler");
  };
}(jQuery), function() {
  /**
   * @param {?} self
   * @param {!Object} value
   * @param {string} x
   * @return {undefined}
   */
  function construct(self, value, x) {
    if (value) {
      /** @type {!Object} */
      self._date = value;
    }
    if (x) {
      /** @type {string} */
      self._mode = x;
    }
  }
  /** @type {function(!Object, !Object): undefined} */
  var select_id = scheduler.setCurrentView;
  /** @type {function(!Object, string): undefined} */
  var target = scheduler.updateView;
  /** @type {null} */
  var hoverSelectionTimeout = null;
  /** @type {null} */
  var watchCountTimeout = null;
  /**
   * @param {!Object} value
   * @param {string} name
   * @return {undefined}
   */
  var test = function(value, name) {
    var self = this;
    window.clearTimeout(watchCountTimeout);
    window.clearTimeout(hoverSelectionTimeout);
    var status = self._date;
    var err = self._mode;
    construct(this, value, name);
    /** @type {number} */
    watchCountTimeout = setTimeout(function() {
      return self.callEvent("onBeforeViewChange", [err, status, name || self._mode, value || self._date]) ? (target.call(self, value, name), self.callEvent("onViewChange", [self._mode, self._date]), window.clearTimeout(hoverSelectionTimeout), void(watchCountTimeout = 0)) : void construct(self, status, err);
    }, scheduler.config.delay_render);
  };
  /**
   * @param {!Object} name
   * @param {boolean} callback
   * @return {undefined}
   */
  var destroy = function(name, callback) {
    var n = this;
    /** @type {!Arguments} */
    var arg = arguments;
    construct(this, name, callback);
    window.clearTimeout(hoverSelectionTimeout);
    /** @type {number} */
    hoverSelectionTimeout = setTimeout(function() {
      if (!watchCountTimeout) {
        target.apply(n, arg);
      }
    }, scheduler.config.delay_render);
  };
  scheduler.attachEvent("onSchedulerReady", function() {
    if (scheduler.config.delay_render) {
      /** @type {function(!Object, string): undefined} */
      scheduler.setCurrentView = test;
      /** @type {function(!Object, boolean): undefined} */
      scheduler.updateView = destroy;
    } else {
      /** @type {function(!Object, !Object): undefined} */
      scheduler.setCurrentView = select_id;
      /** @type {function(!Object, string): undefined} */
      scheduler.updateView = target;
    }
  });
}();
