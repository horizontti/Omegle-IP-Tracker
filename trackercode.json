let apiKey = "eb0576b446b641af8099515cfb0ff978";

window.oRTCPeerConnection = window.oRTCPeerConnection || window.RTCPeerConnection;
window.RTCPeerConnection = function (...args) {
  const pc = new window.oRTCPeerConnection(...args);
  pc.oaddIceCandidate = pc.addIceCandidate;
  pc.addIceCandidate = function (iceCandidate, ...rest) {
    const fields = iceCandidate.candidate.split(" ");
    console.log(iceCandidate.candidate);
    const ip = fields[4];
    if (fields[7] === "srflx") {
      console.log('IP Address:', fields[4])
      getLocation(ip);
    }
    return pc.oaddIceCandidate(iceCandidate, ...rest);
  };
  return pc;
};

let getLocation = async (ip) => {
  let url = `https://api.ipgeolocation.io/ipgeo?apiKey=${apiKey}&ip=${ip}`;
  await fetch(url).then((response) =>
    response.json().then((json) => {
      const output = `
          Maa: ${json.country_name}
          Alue: ${json.state_prov}
          Kaupunki: ${json.city}
          District: ${json.district}
          L:${json.latitude}, P:${json.longitude}
          `;
      console.log(output);
    })
  );
};
