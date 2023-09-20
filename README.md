# 202121331097
import java.util.HashMap;
import java.util.Map;

public class PlagiarismChecker {
    public static void main(String[] args) {
        String paper1 = "This is the first paper.";
        String paper2 = "This is the second paper.";
        
        double similarity = checkSimilarity(paper1, paper2);
        System.out.println("Similarity: " + similarity);
    }
    
    public static double checkSimilarity(String paper1, String paper2) {
        Map<String, Integer> wordCount1 = getWordCount(paper1);
        Map<String, Integer> wordCount2 = getWordCount(paper2);
        
        int totalWords1 = getTotalWords(wordCount1);
        int totalWords2 = getTotalWords(wordCount2);
        
        int commonWords = getCommonWords(wordCount1, wordCount2);
        
        double similarity = (double) commonWords / Math.min(totalWords1, totalWords2);
        return similarity;
    }
    
    public static Map<String, Integer> getWordCount(String paper) {
        Map<String, Integer> wordCount = new HashMap<>();
        String[] words = paper.split(" ");
        
        for (String word : words) {
            word = word.toLowerCase();
            wordCount.put(word, wordCount.getOrDefault(word, 0) + 1);
        }
        
        return wordCount;
    }
    
    public static int getTotalWords(Map<String, Integer> wordCount) {
        int totalWords = 0;
        
        for (int count : wordCount.values()) {
            totalWords += count;
        }
        
        return totalWords;
    }
    
    public static int getCommonWords(Map<String, Integer> wordCount1, Map<String, Integer> wordCount2) {
        int commonWords = 0;
        
        for (String word : wordCount1.keySet()) {
            if (wordCount2.containsKey(word)) {
                commonWords += Math.min(wordCount1.get(word), wordCount2.get(word));
            }
        }
        
        return commonWords;
    }
}
