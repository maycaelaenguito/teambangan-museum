<template>
  <div id="app" class="digital-museum">
    <div class="hide">
      <h4>Sorry, this musuem is not accessible to your device. Open it on bigger devices. 1280px above.</h4>
    </div>
    <!-- Header Section -->
    <section class="museum-header">
      <h1>Welcome to Ocho-ocho Digital Museum</h1>
      <div class="h-description">
        <p>
          Discover the vibrant heart of Philippine popular culture. Our digital
          museum celebrates iconic moments, cherished stories, and timeless
          creativity that define our shared identity. Explore and relive the
          spirit of the Filipinos.
        </p>
      </div>
      <button class="header-btn" @click="scrollToNextSectionFromHeader">
        <svg xmlns="http://www.w3.org/2000/svg" width="40" height="40" fill="currentColor" class="bi bi-chevron-double-down" viewBox="0 0 16 16">
          <path fill-rule="evenodd" d="M1.646 6.646a.5.5 0 0 1 .708 0L8 12.293l5.646-5.647a.5.5 0 0 1 .708.708l-6 6a.5.5 0 0 1-.708 0l-6-6a.5.5 0 0 1 0-.708"/>
          <path fill-rule="evenodd" d="M1.646 2.646a.5.5 0 0 1 .708 0L8 8.293l5.646-5.647a.5.5 0 0 1 .708.708l-6 6a.5.5 0 0 1-.708 0l-6-6a.5.5 0 0 1 0-.708"/>
        </svg>
      </button>
    </section>

    <!-- Main Title Section -->
    <section id="group-section" class="group-section">
      <div class="group-name">
          <h1>{{ groupName }}</h1>
          </div>
          <div class="group-members">
            <span v-for="(member, index) in groupMembers" :key="index">
              {{ member }}
            </span>
          </div>
        </section>

        <!-- Content Sections -->
        <section class="sections-container">
          <div
            v-for="(section, sectionIndex) in sections"
            :key="sectionIndex"
            class="museum-section"
            :style="{
              ...getBackgroundStyle(sectionIndex),
              minHeight: '100vh',
            }"
          >
      <h3>{{ section.title }}</h3>
      <div class="subsections">
        <div
          v-for="(subsection, subsectionIndex) in section.subsections"
          :key="subsectionIndex"
          class="subsection"
          :style="{ backgroundImage: `url(${subsection.image})` }"
          @click="openVirtualRoom(sectionIndex, subsectionIndex)"
        >
          <div class="subsection-title">{{ subsection.title }}</div>
          <button @click="openVirtualRoom(sectionIndex, subsectionIndex)">
            Check Out Room
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="30"
              height="30"
              fill="currentColor"
              class="bi bi-arrow-right-short"
              viewBox="0 0 16 16"
            >
              <path
                fill-rule="evenodd"
                d="M4 8a.5.5 0 0 1 .5-.5h5.793L8.146 5.354a.5.5 0 1 1 .708-.708l3 3a.5.5 0 0 1 0 .708l-3 3a.5.5 0 0 1-.708-.708L10.293 8.5H4.5A.5.5 0 0 1 4 8"
              />
            </svg>
          </button>
        </div>
      </div>
    </div>


    </section>

    <!-- Virtual Room Modal -->
    <div v-if="showModal" class="modal-overlay" @click.self="closeVirtualRoom">
      <div class="modal-content">
        <h3>{{ activeRoom.title }}</h3>
        <p class="description">{{ activeRoom.description }}</p>
        <div class="images-container">
          <img
            v-for="(image, index) in activeRoom.images"
            :key="index"
            :src="image"
            alt="Subsection image"
            class="modal-image"
          />
        </div>
        <button class="close-modal" @click="closeVirtualRoom">Close</button>
      </div>
    </div>
  </div>
</template>


<script>
export default {
  data() {
    return {
      groupName: "Built and Presented by Teambangan",
      groupMembers: [
        "Jhan Philippe Moloa",
        "Maycaela Enguito",
        "Jael Emmanuel Santos",
        "Lilian Josephine Nitura",
        "Mhaydz Jeanette Caparan",
      ],
      sections: [
        {
          title: "Affect Senses & Feelings",
          subsections: [
          {
              title: "The Wowowee Stampede",
              image: require("@/assets/section 1/1.png"),
              description:
                "The PhilSports Stadium Stampede (also referred to as the ULTRA stampede or the Wowowee stampede) was a crowd crush that occurred at the PhilSports Stadium (also known as the ULTRA) in Pasig, Metro Manila in the Philippines on February 4, 2006. It killed 73 people and injured about 400. About 30,000 people had gathered outside the stadium waiting to participate in the first anniversary episode of the former television variety show Wowowee.",
              images: [
              require("@/assets/gallery 1/1_16a082288a7.1665217_806339932_16a082288a7_large.jpg"),
              require("@/assets/gallery 1/wow1.jpg"),
              require("@/assets/gallery 1/tumblr_lg1uo4cmWY1qzeq3qo1_540.jpg"),
              ],
            },
            {
              title: "Bagyong Milenyo",
              image: require("@/assets/section 1/2.png"),
              description: "Bagyong Milenyo, or Typhoon Xangsane, was a devastating tropical cyclone that struck the Philippines in September 2006. It caused widespread destruction in Luzon, resulting in severe flooding, significant infrastructure damage, and loss of life, highlighting disaster preparedness challenges. Bagyong Milenyo (Typhoon Xangsane) struck the Philippines from September 25-29, 2006, causing extensive damage and 213 fatalities. It affected over 4 million people, particularly in Metro Manila, with losses totaling P6.6 billion. The typhoon highlighted safety issues with billboards, leading to their removal after fatalities caused by falling structures",
              images: [
              require("@/assets/gallery 1/bgm1.jpg"),
              require("@/assets/gallery 1/bgm2.jpg"),
              require("@/assets/gallery 1/bgm3.jpg"),
              ],
            },
            {
              title: "Philippine Airlines Flight 812",
              image: require("@/assets/section 1/3.png"),
              description: "On May 25, 2000, Philippine Airlines Flight 812 was hijacked before landing in Manila. Armed with a gun and a grenade, the hijacker demanded valuables and attempted to escape via a homemade parachute. He died three days later when the parachute failed to deploy. Reginald Chua hijacked Philippine Airlines Flight 812, citing family abandonment as his motivation. Armed with a pistol and grenade, he demanded money before attempting to escape via parachute. His behavior during the incident raised concerns about his mental health, and his body was later found in Quezon.",
              images: [
              require("@/assets/gallery 1/pal1.jpg"),
              require("@/assets/gallery 1/pal2.jpg"),
              require("@/assets/gallery 1/pal3.jpg"),
              ],
            },
          ],
          
        },
        {
          title: "Body and Self Image",
          subsections: [
          {
              title: "Miss International 2005 Victory",
              image: require("@/assets/section 2/2005-miss-international-winner-philippines-precious-lara-550nw-7828522e.jpg"),
              description:
                "In 2005, Precious Lara Quigaman’s Miss International win celebrated diverse Filipino beauty and sparked national pride. This victory shifted the focus from traditional beauty standards to a more inclusive view, highlighting intelligence and cultural identity, ultimately reshaping self-image in Philippine popular culture during the decade. Precious Lara’s Miss International win in 2005 influenced Philippine popular culture by promoting a broader definition of beauty. It encouraged self-acceptance and highlighted the importance of intelligence and cultural identity, leading to a more inclusive perspective on body image and self-worth during the 2000s.",
                images: [
                require("@/assets/gallery 2/2005-miss-international-winner-philippines-precious-lara-550nw-7828522b.jpg"),
                require("@/assets/gallery 2/845806bf9c531275af1bae331f79383a.jpg"),
                require("@/assets/gallery 2/1659413732_966318566_16_ent.png"),
                ],
            },
            {
              title: "Marian Rivera crowned as FHM Philippines' Sexiest Woman for 2008",
              image: require("@/assets/section 2/fhm_main.jpg"),
              description: "Marian Rivera's rise to fame through her role in the hit show Marimar led to her crowning as FHM Philippines' Sexiest Woman in 2008. This victory not only celebrated her beauty but also brought the FHM awards into Philippine households, elevating the magazine's profile and influencing popular culture. Rivera's win showcased a blend of talent and attractiveness, encouraging greater acceptance of diverse beauty standards in the process. Marian Rivera's FHM win in 2008 influenced Philippine popular culture by reinforcing beauty ideals that emphasized physical appearance. While she inspired body positivity, it also risked promoting unrealistic standards among young fans, potentially impacting their self-image and leading to pressure to conform to these ideals.",
              images: [
              require("@/assets/gallery 2/mar1.jpg"),
              require("@/assets/gallery 2/mar2.jpg"),
              require("@/assets/gallery 2/mar3.webp"),
              ],
            },
            {
              title: "Emo Culture",
              image: require("@/assets/section 2/2000s-pop-punk-emo-culture-collage_818261-41677.avif"),
              description: "Emo culture in the 2000s reshaped Philippine popular culture by promoting individuality and emotional expression. It influenced body image through distinctive fashion choices and encouraged discussions about mental health, allowing youth to embrace vulnerability and authenticity, ultimately transforming self-image and perceptions of beauty during the decade. Emo culture in the 2000s empowered Filipino youth by promoting individuality and personal expression. It encouraged them to embrace their unique identities and emotions, challenging societal norms and fostering a sense of belonging within a community that valued authenticity and diverse self-representation.",
              images: [
              require("@/assets/gallery 2/emo1.jpg"),
              require("@/assets/gallery 2/emo2.jpg"),
              require("@/assets/gallery 2/emo3.jpg"),
              ],
            },
          ],
        },
        {
          title: "Space",
          subsections: [
            {
              title: "The opening of SM Mall of Asia",
              image: require("@/assets/section 3/sm-mall-of-asia-4672.jpg"),
              description:
                "The opening of SM Mall of Asia in 2006 transformed Philippine popular culture by redefining public space. As a major hub for shopping, dining, and entertainment, it fostered social interaction and showcased modernity, becoming a significant cultural landmark that shaped leisure and lifestyle for many Filipinos. The opening of SM Mall of Asia in the 2000s created a dynamic venue for Filipinos, encouraging social gatherings and recreational activities. It became a cultural landmark that enriched shopping and entertainment experiences, reflecting the country's evolving consumer culture and serving as a central hub for families and youth.",
                images: [
                require("@/assets/gallery 3/moa1.jpg"),
                require("@/assets/gallery 3/moa2.jpg"),
                require("@/assets/gallery 3/moa3.jpg"),
                ],
            },
            {
              title: "PBCom Tower",
              image: require("@/assets/section 3/pbcom-original-main.jpg"),
              description: "The PBCom Tower, completed in 2000, became a symbol of modernity and economic growth in the Philippines. As the tallest building in the country at the time, it represented the rise of urban development and corporate culture, reflecting the aspirations of Filipinos during the early 2000s. The building’s completion in the 2000s inspired a sense of national pride and ambition among Filipinos. As a symbol of progress and urbanization, it represented the country's growing economy and modern identity, motivating people to aspire for success and contributing to the development of Metro Manila.",
              images: [
              require("@/assets/gallery 3/pbcom1.jpg"),
              require("@/assets/gallery 3/pbcom2.jpg"),
              require("@/assets/gallery 3/pbcom3.jpg"),
              ],
            },
            {
              title: "Manila Ocean Park",
              image: require("@/assets/section 3/ManilaOceanParkAttractionsPass-KlookIndia.jpg"),
              description: "Manila Ocean Park, opened in 2008, was the first marine-themed park in the Philippines, merging entertainment and education. It showcased marine biodiversity and promoted environmental awareness, reflecting a growing appreciation for conservation. Its unique attractions emphasized family-oriented recreation and enhanced the cultural landscape of the country. This impacted the Philippines by boosting tourism and enhancing the country’s reputation as a marine destination. It attracted local and international visitors, supporting the economy through increased spending in hospitality and related services. The park also raised awareness of marine conservation, encouraging educational initiatives and fostering a greater appreciation for biodiversity, thus contributing to the cultural and environmental landscape of the nation.",
              images: [
              require("@/assets/gallery 3/oc1.jpg"),
              require("@/assets/gallery 3/oc2.webp"),
              require("@/assets/gallery 3/oc3.jpg"),
              ],
            },
          ],
        },
        {
          title: "Time",
          subsections: [
            {
              title: "Social Media",
              image: require("@/assets/section 4/socmed.png"),
              description:
                "Early 2000's marked the rapid evolution of social media, transforming how people connected, shared content, and communicated globally. Early platforms like Friendster (2002) and MySpace (2003) introduced the concept of online social networking, with MySpace becoming a cultural phenomenon through customizable profiles and music discovery. Facebook’s launch in 2004 signaled a new era, initially targeting college students but quickly expanding to a global audience. Its introduction of the News Feed in 2006 revolutionized how users consume content, establishing itself as the dominant platform. Meanwhile, LinkedIn (2003) catered to professional networking, and YouTube (2005) became the go-to site for video sharing, redefining entertainment and content creation. The rise of mobile technology, fueled by the iPhone in 2007, made social media more accessible, boosting platforms like Twitter, which popularized real-time updates and hashtags. By 2010, social media had become a global phenomenon, reshaping communication, marketing, and media consumption while sparking conversations about privacy and digital identity.",
              images: [
              require("@/assets/gallery 4/soc1.webp"),
              require("@/assets/gallery 4/soc2.webp"),
              require("@/assets/gallery 4/soc3.webp"),
              ],
            },
            {
              title: "The Maguindanao Massacre",
              image: require("@/assets/section 4/19ampatuan11.jpg"),
              description: "The Maguindanao massacre, also known as the Ampatuan massacre, occurred on November 23, 2009, in the Philippines, and is one of the deadliest incidents of political violence in the country’s history. Fifty-eight people, including 32 journalists, were killed in an ambush tied to a political rivalry between the Ampatuan and Mangudadatu families. The victims were brutally murdered and buried in mass graves, drawing national and international condemnation. The decade-long legal battle ended in 2019 with the conviction of 28 individuals, including key members of the Ampatuan clan, who were sentenced to life imprisonment. The massacre remains a chilling reminder of the dangers of political violence and threats to press freedom, commemorated annually to honor the victims and advocate for justice.",
              images: [
              require("@/assets/gallery 4/amp1.webp"),
              require("@/assets/gallery 4/amp2.webp"),
              require("@/assets/gallery 4/amp3.jpg"),
              ],
            },
            {
              title: "Manny “PacMan” Pacquiao",
              image: require("@/assets/section 4/e80523967b8ce95f85f3791c190cacfb-getty-boxing-us-phi-de_la_hoya-pacquiao.jpg"),
              description: "From 2000 to 2010, Manny Pacquiao rose to boxing greatness with landmark victories over legends like Marco Antonio Barrera, Érik Morales, and Juan Manuel Márquez, establishing himself as a dominant force in multiple weight classes. His victory over Oscar De La Hoya in 2008 marked a turning point, propelling him to global stardom.By the end of the decade, Pacquiao had become the first eight-division world champion with emphatic wins over Ricky Hatton and Miguel Cotto. His explosive power, speed, and versatility earned him the title of Fighter of the Decade, cementing his legacy as one of the sport’s all-time greats.",
              images: [
              require("@/assets/gallery 4/pac1.webp"),
              require("@/assets/gallery 4/pac2.webp"),
              require("@/assets/gallery 4/pac3.jpg"),
              ],
            },
          ],
        },
        
        {
          title: "Performance",
          subsections: [
            {
              title: "Charice Pempengco on Oprah",
              image: require("@/assets/section 5/charice-pempengco1-1-d4167078cf3844f580a34bb4518d66ab.jpg"),
              description:
                "Jake Cyrus, formerly known as Charice Pempengco, captivated audiences with her 2008 appearance on The Oprah Winfrey Show, showcasing Filipino talent on a global stage. Her powerful performances inspired national pride and encouraged aspiring artists, marking a significant moment in Philippine popular culture during the 2000s. Jake Cyrus's 2008 appearance on Oprah instilled a deep sense of pride among Filipino youth, as they saw one of their own achieving global recognition. This milestone inspired them to embrace their cultural identity and aspire to showcase their talents on an international stage.",
              images: [
              require("@/assets/gallery 5/char1.jpg"),
              require("@/assets/gallery 5/char2.jpg"),
              require("@/assets/gallery 5/char3.jpg"),
              ],
            },
            {
              title: "Local Films like Magnifico, One More Chance, & Tanging Yaman",
              image: require("@/assets/section 5/MV5BNWQ3OGU2NmYtZjY5OC00Yjc1LTg3ZGEtZTlkY2YzNjE5NjA3XkEyXkFqcGc@._V1_.jpg"),
              description: "The success of local films like Magnifico, One More Chance, and Tanging Yaman in the 2000s showcased powerful performances and emphasized family values. These movies resonated with audiences, fostering cultural pride and identity while elevating Philippine cinema as a significant force in the entertainment landscape during the decade. The success of local films in the 2000s instilled a sense of accomplishment as these award-winning movies garnered international recognition. This achievement fostered pride among Filipinos, motivating them to celebrate their cultural contributions and engage more deeply with their heritage.",
              images: [
              require("@/assets/gallery 5/fil1.webp"),
              require("@/assets/gallery 5/fil2.jpg"),
              require("@/assets/gallery 5/fil3.jpg"),
              ],
            },
            {
              title: "Sexbomb Girls - The Spageti Song",
              image: require("@/assets/section 5/spag.jpg"),
              description: "The Sexbomb Girls rose to fame through their appearances on Eat Bulaga in the 2000s, captivating audiences with their hit 'The Spaghetti Song'. Their catchy music, playful choreography, and humor celebrated fun and lightheartedness, significantly impacting Philippine popular culture and evolving standards of femininity.",
              images: [
              require("@/assets/gallery 5/spag1.jpg"),
              require("@/assets/gallery 5/spag2.jpg"),
              require("@/assets/gallery 5/spag3.webp"),
              ],
            },
          ],
        },
        {
          title: "Technology",
          subsections: [
            {
              title: "NBN-ZTE Scandal",
              image: require("@/assets/section 6/zte.jpg"),
              description:
                "The NBN-ZTE Scandal unravelled in the Philippines in 2007, epitomising the pernicious pitfalls of bureaucracy entwined with corruption. The controversy revolved around a $329-million National Broadband Network contract awarded to ZTE Corporation, mired by clandestine collusion and allegations of political perfidy. Lacerated by dissidence, the deal was scrutinised for its exorbitant cost and lack of transparency, exposing a dissonance between public interest and political priorities, which counter-obeisantly begets into painting a picture of systemic malfeasance through accusations of bribes, including kickbacks involving high-ranking officials. Chronologging the fallout, the incident fueled a fervour of protests and demand for deliverance from corruption’s grip. The NBN-ZTE Scandal remains a bellwether for administrative reform, serving as a discursive crucible for anti-corruption initiatives, especially given, at present, in an era of heightened scrutiny, such scandals have cultivated a penchant for greater deference to transparency and accountability measures. However, the pervasive persistence of systemic fragilities continues to pose significant challenges, as obsolete practices and institutional inertia enervate reform initiatives. The scandal’s legacy, juxtaposed against modern digitalisation endeavours, emphasises an enduring imperative for safeguarding public trust and dismantling systemic malpractices.",
              images: [
              require("@/assets/gallery 6/zte1.jpg"),
              require("@/assets/gallery 6/zte2.jpg"),
              require("@/assets/gallery 6/zte3.jpg"),
              ],
            },
            {
              title: "The ILOVEYOU Virus",
              image: require("@/assets/section 6/7aab822f-c2d9-4f96-9198-6c03d3e8a10a_596x562.jpg"),
              description: "The ILOVEYOU virus, an archetypal example of a catastrophic cybersecurity conundrum, emerged on May 4, 2000, as a furtive and insidious malware attack originating in the Philippines. It exploited human proclivity for emotional vulnerability, spreading via email with the subject line “ILOVEYOU” and an attached file masquerading as a benign text document. Upon opening, the script unleashed a digital deluge that corrupted data, overwrote files, and propagated itself to all contacts in the victim's address book; this machination, fueled by naïve trust in technology, caused widespread fragmentation of global IT infrastructure, crippling systems from corporations to governments. Its impact was both egregious and inexorable, with damages estimated to exceed $10 billion globally, exposing the defenceless state of early 2000s cybersecurity protocols. Today, the ILOVEYOU virus serves as an evocative cautionary tale in the age of increasingly esoteric and labyrinthine cyber threats. While modern systems boast resilience through advanced firewalls, heuristic algorithms, and AI-driven defences, the dissonance between technological progress and user education remains a persistent predicament. The virus’s legacy underscores the need to amalgamate robust security measures with a heightened awareness of social engineering tactics. The rise of benign-looking phishing attacks and ransomware demonstrates the dialectic of innovation versus exploitation, where attackers exploit the same ineffable connectivity that drives progress. In a setting often beleaguered by resource constraints, the fight against cyber threats demands magnanimous collaboration and vigilance to avoid repeating the anachronistic errors of the past.",
              images: [
              require("@/assets/gallery 6/ily1.webp"),
              require("@/assets/gallery 6/ily2.webp"),
              require("@/assets/gallery 6/ily3.jpg"),
              ],
            },
            {
              title: "Mobile Phones",
              image: require("@/assets/section 6/360_F_69377756_QBf3gfSHB3hXoGkscIeB9yi2oNEBYrip.jpg"),
              description: "From 2000 to 2010, mobile phones evolved from basic feature phones to advanced smartphones. Early in the decade, brands like Nokia and Motorola dominated with compact designs, SMS/MMS messaging, and basic cameras, while 2G and 3G networks enabled faster browsing and email. Stylish devices like the Motorola Razr set trends, and multimedia features like Bluetooth and MP3 players became standard. The late 2000s saw the smartphone revolution with the launch of the iPhone (2007) and Android (2008). Touchscreens, app stores, GPS, and faster 3G networks transformed phones into all-in-one devices for browsing, social media, and entertainment, paving the way for modern mobile technology.",
              images: [
              require("@/assets/gallery 6/mob1.webp"),
              require("@/assets/gallery 6/mob2.webp"),
              require("@/assets/gallery 6/mob3.jpg"),
              ],
            },
          ],
        },
      ],
      
      showModal: false,
      activeRoom: {},
    };
  },
  mounted() {
    const appContainer = document.getElementById("app");
    appContainer.addEventListener("wheel", this.handleMouseWheel, {
      passive: false,
    });
  },
  beforeUnmount() {
    const appContainer = document.getElementById("app");
    appContainer.removeEventListener("wheel", this.handleMouseWheel);
  },
  methods: {
    getBackgroundStyle(index) {
      const backgrounds = [
        { type: 'image', value: require("@/assets/bg-retro-3.png")},
        { type: 'image', value: require("@/assets/bg/2.png")},
        { type: 'image', value: require("@/assets/bg/3.png")},
        { type: 'image', value: require("@/assets/bg/4.png")},
        { type: 'image', value: require("@/assets/bg/5.png")},
        { type: 'image', value: require("@/assets/bg/6.png")}, 
      ];

      const bg = backgrounds[index % backgrounds.length]; // Cycle through backgrounds

      if (bg.type === 'color') {
        return { backgroundColor: bg.value }; // Return background color style
      } else if (bg.type === 'image') {
        return {
          backgroundImage: `url(${bg.value})`,
          backgroundSize: 'cover',
          backgroundRepeat: 'no-repeat',
          backgroundPosition: 'center',
        }; // Return background image style
      }

      return { backgroundColor: '#FFFFFF' }; // Default fallback
    },
    scrollToNextSectionFromHeader() {
      const target = document.getElementById("group-section"); // Ensure ID matches
      if (target) {
        target.scrollIntoView({ behavior: "smooth" }); // Smooth scrolling
      }
    },
    openVirtualRoom(sectionIndex, subsectionIndex) {
      this.activeRoom =
        this.sections[sectionIndex].subsections[subsectionIndex];
      this.showModal = true;
    },
    closeVirtualRoom() {
      this.showModal = false;
      this.activeRoom = {};
    },
    handleMouseWheel(event) {
      event.preventDefault(); // Prevent default scroll behavior
      const scrollAmount = event.deltaY > 0 ? 100 : -100; // Adjust scroll speed
      window.scrollBy({
        top: scrollAmount,
        behavior: "smooth", // Smooth scrolling
      });
    },
  },

};
</script>


<style src="./styles.css"></style>
