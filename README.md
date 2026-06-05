<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>🌴 Dream Trip Planner – Your Perfect Vacation Awaits</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <script src="https://cdn.jsdelivr.net/npm/marked/marked.min.js"></script>
  <script src="https://unpkg.com/lucide@latest"></script>
  <style>
    html,body{margin:0;padding:0;height:100%;overflow-x:hidden;}
    body{
      font-family:'Poppins',sans-serif;
      background:linear-gradient(135deg,#a8edea 0%,#fed6e3 100%);
      color:#0f172a;
    }
    .glass{
      background:rgba(255,255,255,0.7);
      backdrop-filter:blur(14px);
      border:1px solid rgba(255,255,255,0.4);
      box-shadow:0 10px 40px rgba(0,0,0,0.08);
    }
    .header-banner{
      background:linear-gradient(90deg,#00b4d8,#48cae4,#90e0ef);
      color:white;
      padding:2rem;
      border-bottom-left-radius:3rem;
      border-bottom-right-radius:3rem;
      box-shadow:0 8px 30px rgba(0,0,0,0.15);
    }
    .gradient-text{
      background:linear-gradient(90deg,#0284c7,#14b8a6,#f97316);
      -webkit-background-clip:text;
      -webkit-text-fill-color:transparent;
    }
    .btn-modern{
      background:linear-gradient(90deg,#14b8a6,#06b6d4,#3b82f6);
      color:white;
      box-shadow:0 6px 20px rgba(14,165,233,0.3);
      transition:transform 0.1s ease-in,box-shadow 0.2s ease-in;
    }
    .btn-modern:hover{transform:translateY(-2px);box-shadow:0 10px 25px rgba(14,165,233,0.4);}
    .icon-label{display:flex;align-items:center;gap:0.5rem;color:#0369a1;font-weight:500;}
    .input-box{
      background:white;border:1px solid #dbeafe;border-radius:0.75rem;
      padding:0.75rem;box-shadow:inset 0 0 10px rgba(0,0,0,0.03);width:100%;
    }
    .spinner{
      border:4px solid rgba(0,0,0,0.05);border-left-color:#14b8a6;
      width:30px;height:30px;border-radius:50%;animation:spin 1s linear infinite;
    }
    @keyframes spin{to{transform:rotate(360deg);}}
    .output-prose a{color:#0284c7;text-decoration:underline;}
  </style>
</head>

<body>
  <header class="header-banner text-center">
    <h1 class="text-5xl font-extrabold mb-2 flex items-center justify-center gap-3">
      <i data-lucide="globe-2" class="w-10 h-10 text-white"></i> Dream Trip Planner
    </h1>
    <p class="text-lg opacity-90">Plan your perfect escape — let AI craft your itinerary 🌍✨</p>
  </header>

  <div class="container mx-auto px-6 py-10">
    <div class="grid lg:grid-cols-12 gap-10 items-start">
      <!-- Left Form -->
      <section class="lg:col-span-6">
        <div class="glass rounded-3xl p-8">
          <h2 class="text-2xl font-semibold gradient-text mb-4 flex items-center gap-2">
            <i data-lucide="map-pin" class="w-6 h-6"></i> Customize Your Trip
          </h2>

          <form id="travel-form" class="grid grid-cols-1 gap-4">
            <div class="icon-label"><i data-lucide="plane" class="w-5 h-5"></i>Destination</div>
            <input id="location" type="text" placeholder="Where to? (e.g., Bali, Paris)" class="input-box"/>

            <div class="icon-label"><i data-lucide="calendar" class="w-5 h-5"></i>Trip Duration</div>
            <input id="days" type="number" min="1" placeholder="Days (e.g., 5)" class="input-box"/>

            <div class="icon-label"><i data-lucide="clock" class="w-5 h-5"></i>When are you traveling?</div>
            <input id="travelTime" type="text" placeholder="e.g., December 2025" class="input-box"/>

            <div class="icon-label"><i data-lucide="wallet" class="w-5 h-5"></i>Budget</div>
            <input id="budget" type="number" min="0" placeholder="Budget ₹" class="input-box"/>

            <div class="icon-label"><i data-lucide="bed" class="w-5 h-5"></i>Type of Room</div>
            <select id="roomType" class="input-box">
              <option value="">Select room type</option>
              <option>Standard</option><option>Deluxe</option><option>Suite</option>
              <option>Villa</option><option>Budget / Hostel</option>
            </select>

            <div class="icon-label"><i data-lucide="car" class="w-5 h-5"></i>Vehicle & Driver</div>
            <select id="vehicle" class="input-box">
              <option value="">Need a driver?</option><option>Yes</option><option>No</option>
            </select>

            <div class="icon-label"><i data-lucide="map" class="w-5 h-5"></i>Tourist Guide</div>
            <select id="guide" class="input-box">
              <option value="">Need a guide?</option><option>Yes</option><option>No</option>
            </select>

            <div class="icon-label"><i data-lucide="sparkles" class="w-5 h-5"></i>Experience Type</div>
            <select id="experience" class="input-box">
              <option value="">Choose an experience</option>
              <option>Adventure</option><option>Relaxation</option><option>Culture</option>
              <option>Nature</option><option>Luxury</option><option>Budget-friendly</option>
            </select>

            <div class="icon-label"><i data-lucide="train" class="w-5 h-5"></i>Preferred Transport</div>
            <select id="transport" class="input-box">
              <option value="">Select transport</option>
              <option>Car</option><option>Bus</option><option>Train</option>
              <option>Flight</option><option>Bike/Scooter</option>
            </select>

            <div class="icon-label"><i data-lucide="users" class="w-5 h-5"></i>Travel Companions</div>
            <select id="companions" class="input-box">
              <option value="">Who are you traveling with?</option>
              <option>Solo</option><option>Couple</option><option>Family</option>
              <option>Friends</option><option>Group Tour</option>
            </select>

            <textarea id="prompt" rows="4" placeholder="Anything special you'd like? (e.g., scuba diving, local food)" class="input-box"></textarea>

            <button id="generateBtn" type="submit" class="btn-modern rounded-xl py-3 font-semibold flex items-center justify-center gap-2 text-lg mt-2">
              <i data-lucide="sparkle" class="w-5 h-5"></i> Generate My Trip Plans 🌴
            </button>
          </form>

          <div id="loader" class="hidden mt-5 flex items-center gap-3 text-slate-700">
            <div class="spinner"></div> Crafting your dream vacation...
          </div>
          <div id="error" class="hidden mt-3 text-sm text-red-700 bg-red-50 p-3 rounded-xl border border-red-100"></div>
        </div>
      </section>

      <!-- Right Display -->
      <aside class="lg:col-span-6">
        <div class="glass rounded-3xl p-6 h-full flex flex-col">
          <h2 class="text-xl font-semibold text-slate-800 flex items-center gap-2 mb-3">
            <i data-lucide="sun" class="w-5 h-5 text-amber-500"></i> Choose Your Adventure
          </h2>
          <div id="optionsContainer" class="grid grid-cols-1 md:grid-cols-2 gap-4"></div>

          <div id="comparisonOutput" class="hidden mt-6 bg-white/70 rounded-xl p-4 shadow-inner prose max-w-none"></div>

          <div id="output" class="hidden mt-4 output-prose overflow-auto prose max-w-none p-4 bg-white/70 rounded-xl shadow-inner"></div>
        </div>
      </aside>
    </div>
  </div>

  <script>
    lucide.createIcons();

    const form = document.getElementById("travel-form");
    const outputDiv = document.getElementById("output");
    const loader = document.getElementById("loader");
    const errorBox = document.getElementById("error");
    const optionsContainer = document.getElementById("optionsContainer");
    const comparisonOutput = document.getElementById("comparisonOutput");

    // 🔒 Replace this with your real key from https://openrouter.ai/settings/keys
    const apiKey = "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"; 
    const baseURL = "https://openrouter.ai/api/v1";

    function showLoader(){ loader.classList.remove("hidden"); }
    function hideLoader(){ loader.classList.add("hidden"); }
    function showError(msg){ errorBox.textContent = msg; errorBox.classList.remove("hidden"); }
    function hideError(){ errorBox.classList.add("hidden"); }

    async function getTripPlans(prompt){
      const response = await fetch(`${baseURL}/chat/completions`, {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
          "Authorization": `Bearer ${apiKey}`,
          "HTTP-Referer": "https://yourdomain.com",
          "X-Title": "Trip Planner"
        },
        body: JSON.stringify({
          model: "openai/gpt-4o-mini",
          messages: [
            {role: "system", content: "You are Trip Planner AI. Generate TWO completely distinct trip itineraries: Plan A 🌞 and Plan B 🌙. Each must include: 1) daily plan, 2) attractions, 3) food, 4) accommodation, 5) estimated cost in INR, and 6) summary paragraph. Use markdown and emojis."},
            {role: "user", content: prompt}
          ]
        })
      });
      if(!response.ok){
        const errText = await response.text();
        throw new Error(`API error ${response.status}: ${errText}`);
      }
      const data = await response.json();
      return data.choices?.[0]?.message?.content || "";
    }

    async function getPlanDifference(planA, planB){
      const prompt = `Compare these two travel plans in a concise markdown table and short summary paragraph. Focus on differences in destination highlights, experiences, accommodation, transportation, and cost.\n\nPlan A:\n${planA}\n\nPlan B:\n${planB}`;
      const response = await fetch(`${baseURL}/chat/completions`, {
        method: "POST",
        headers: {"Content-Type": "application/json","Authorization": `Bearer ${apiKey}`},
        body: JSON.stringify({
          model: "openai/gpt-4o-mini",
          messages: [
            {role: "system", content: "You are a travel comparison expert."},
            {role: "user", content: prompt}
          ]
        })
      });
      const data = await response.json();
      return data.choices?.[0]?.message?.content || "Could not generate comparison.";
    }

    form.addEventListener("submit", async (e)=>{
      e.preventDefault();
      hideError();
      outputDiv.classList.add("hidden");
      comparisonOutput.classList.add("hidden");
      optionsContainer.innerHTML = "";
      showLoader();

      const location = document.getElementById("location").value;
      const days = document.getElementById("days").value;
      const travelTime = document.getElementById("travelTime").value;
      const budget = document.getElementById("budget").value;
      const roomType = document.getElementById("roomType").value;
      const vehicle = document.getElementById("vehicle").value;
      const guide = document.getElementById("guide").value;
      const experience = document.getElementById("experience").value;
      const transport = document.getElementById("transport").value;
      const companions = document.getElementById("companions").value;
      const promptText = document.getElementById("prompt").value;

      const fullPrompt = `
      Create TWO very different ${days}-day trip plans for ${location} in ${travelTime}, with a budget of ₹${budget}.
      Room Type: ${roomType}. Vehicle: ${vehicle}. Guide: ${guide}.
      Experience: ${experience}. Transport: ${transport}. Companions: ${companions}.
      Special preferences: ${promptText}.
      Label them clearly as 'Plan A 🌞' and 'Plan B 🌙'.`;

      try {
        const responseText = await getTripPlans(fullPrompt);
        await renderOptions(responseText);
      } catch (err) {
        showError(err.message);
      } finally {
        hideLoader();
      }
    });

    async function renderOptions(markdownText){
      const planARegex = /(Plan\s*A[\s\S]*?)(?=Plan\s*B|$)/i;
      const planBRegex = /(Plan\s*B[\s\S]*)/i;
      const planAMatch = markdownText.match(planARegex);
      const planBMatch = markdownText.match(planBRegex);
      let planA = planAMatch ? planAMatch[1] : "Plan A 🌞\\nYour first amazing plan will go here.";
      let planB = planBMatch ? planBMatch[1] : "Plan B 🌙\\nYour alternative adventure awaits here.";
      optionsContainer.innerHTML = "";

      [planA, planB].forEach((plan, i)=>{
        const card = document.createElement("div");
        card.className = "glass rounded-2xl p-4 bg-gradient-to-br from-sky-50 to-emerald-50 flex flex-col justify-between shadow";
        card.innerHTML = `
          <div class="overflow-auto max-h-80 prose text-sm">${marked.parse(plan)}</div>
          <button class="mt-3 btn-modern text-white py-2 rounded-xl text-sm font-semibold" data-index="${i}">
            Select This Plan 💼
          </button>`;
        optionsContainer.appendChild(card);
      });

      const diffText = await getPlanDifference(planA, planB);
      comparisonOutput.innerHTML = `<h3 class="text-lg font-semibold mb-2">🔍 Comparison: Plan A vs Plan B</h3>${marked.parse(diffText)}`;
      comparisonOutput.classList.remove("hidden");

      optionsContainer.querySelectorAll("button").forEach(btn=>{
        btn.addEventListener("click", ()=>{
          const index = btn.getAttribute("data-index");
          const chosen = index == "0" ? planA : planB;
          outputDiv.innerHTML = marked.parse(chosen);
          outputDiv.classList.remove("hidden");
          window.scrollTo({top:outputDiv.offsetTop, behavior:"smooth"});
        });
      });
    }
  </script>
</body>
</html>
